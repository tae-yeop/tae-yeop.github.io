---
title:  "생성 모델 2"
excerpt:  "그 동안 공부해온 발자취"
categories: 
- Generative Model

tags:
- Generative Model
 
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-12
---


# 데이터에 따라 다를까?



# 평가 메트릭
애매한 부분에 왔다. classification model의 경우 정확도, FPR 등 정확히 딱 계산되는 평가 메트릭이 있는데 아쉽게도 generative model에선 우리가 인지하는 것과 상반되는 것을 보여주기 때문이다.


여전히 FID는 많이 사용되고 human perception에 매칭되진 않지만 뭔가 향상되는 것을 판단하는데 사용되긴 한다.

사실 기존에 IQA Metrics(Image Quality Assesment)라고 이미지 퀄리티를 평가하는 방법들이 마련되긴 했었다.


대표적인 라이브러리

torch metrics가 있는데 이는 pip install torch-fidelity에 의존함

- https://github.com/layer6ai-labs/dgm-eval
- https://github.com/photosynthesis-team/piq
- https://github.com/toshas/torch-fidelity
- https://github.com/marcojira/fld (2024년 최신)
 FLD(FLS), fld


참고로 평가시에는 `truncation trick` 같은 기법은 off 시켜서 공정한 비교가 되게끔 한다. 


## 이미지 메트릭

이론적인 계산 방식 보다는 오히려 사람한테 직접 물어서 점수를 매기는 Mean Opinion Scroe(MOS)을 쓰기도 한다.

이 때문에 은근히 생성모델은 점수판 없는 축구경기 같은 느낌이기도 하다. 


| Metric | Quality(Fidelity) | Diversity | Latent‑Space Disentangle | Over‑fitting(Memorization) | 원리 / Type | Repo |
|--------| ----------------- | --------- | ------------------------ | -------------------------- | ---------- | -----|
|FID | ✔︎ | ✔︎ |  |  | Fréchet Distance (Inception) | https://github.com/NVlabs/stylegan2-ada-pytorch|
|KID | ✔︎ | ✔︎ |  |  | MMD with Polynomial Kernel | |
|clean‑FID | ✔︎ | ✔︎ |  |  | Dataset‑agnostic Fréchet | https://github.com/GaParmar/clean-fid |
CAFD | ✔︎ | ✔︎ |  | ✔︎ | Class‑Aware FID | https://github.com/B1ueber2y/CAFD
MiFID | ✔︎ | ✔︎ |  | ✔︎ | Mixed‑feature FID (Kaggle) | https://www.kaggle.com/c/gan-getting-started/overview/evaluation
Conditional FID | ✔︎ | ✔︎ |  | ✔︎ | FID (per‑class) | https://github.com/Michael-Soloveitchik/CFID
IS (Inception Score) | ✔︎ | ✔︎ |  |  | KL div. over class posteriors | ^ stylegan2‑ada
PPL (Path Length) | ✔︎ |  | ✔︎ |  | Jacobian norm along latent path | ^ stylegan2‑ada
Improved P&R | ✔︎ | ✔︎ |  |  | Non‑parametric Precision/Recall | https://github.com/kynkaat/improved-precision-and-recall-metric
Density & Coverage | ✔︎ | ✔︎ |  | ✔︎ | k‑NN Precision/Recall variant | https://github.com/clovaai/generative-evaluation-prdc
α‑Precision / β‑Recall | ✔︎ | ✔︎ |  | ✔︎ | Distribution‑free P&R (synthetic tabular) | — (공식 코드 미공개) OpenReview
NND (Neural‑Net Divergences) |  |  |  | ✔︎ | Trainable critic divergence | OpenReview
Data‑Copying Test | ✔︎ |  |  | ✔︎ | Permutation test for duplicates | https://github.com/casey-meehan/data-copying


FID (Frechet Inception Distance)
$$
FID(X_s, X_t) = FD(X_s, X_t, F =\text{InceptionV3}) \\
= ||\mu_{real} - \mu_{fake}||^2_2 + Tr(\Sigma_{real} + \Sigma_{fake} - 2(\Sigma_{real}\Sigma_{fake})^{1/2}) \\
$$
- 진짜 이미지 → Incetption-v3 → high-dimensional feature embedding space_real
- 가짜 이미지 → Incetption-v3 → high-dimensional feature embedding space_fake
- Mean과 Covariace를 각각 계산 : $(\mu_{real}, \Sigma_{real}) , (\mu_{fake}, \Sigma_{fake})$
- mutlivariate gaussian을 얻어낸 embedding space에 fitting시켜서 두 분포의 Frechet Distance 계산
    - mean과 covariance가 유사하다면 갑이 작게 나옴 → FID는 작을 수록 좋다.
- intra-class와 mode collpase를 감지할 수 있음.
- 생성 이미지 분포와 gt 이미지 분포간의 Wasserstein-2 distance를 계산한다.

단점
- Gaussian assumption이 현실에 맞지 않을 수도 있음
- 샘플 사이즈가 적다면 실제 FID보다 over-estimation할 수 있음
- 숫자가 적어지면 bias가 생김
- 이런 bias를 줄이기 위해 생성된 $N$개와 진짜 이미지 전체를 모두 비교에 참여
- biased estimator => 갯수가 적으면 정확하지 않음

실제 계산 방법
- [Martin Heusel et al.](https://papers.nips.cc/paper/2017/hash/8a1d694707eb0fefe65871369074926d-Abstract.html)이 제안한 방법
    - 비교할 때 50K의 생성이미지와 학습에 쓰인 모든 이미지 사이를 비교하였다. (실제로 얼만큼 학습에 사용되었는지 신경 쓰지 않고)
    - 이 방법이 ADA에도 쓰임
- FID_{50K}라고 하면 50K개의 생성된 이미지와 비교를 하는 것임


KID(Kernel Inception Distance)
- Inception Net의 embedding space로 매핑된 진짜 데이터 분포와 가짜 데이터 분포간의 MMD를 계산
- unbiased estimator (갯수가 적더라도 표준편차가 빠르게 줄어듬)
- 작은 규모의 데이터셋에 적합
- 단점은 $O(n^2)$ time complexity (FID는 $O(n)$)


SSIM(Structural Similarity Index)
- 단순히 이미지간의 에러를 계산하는게 아니라 사람이 시각 인지를 할때에는 구조적 정보를 인지하려고 한다.
- 두 이미지에서 나오는 구조 정보와 인지현상 정보의 차이를 이용한다. 3가지 독립적인 특징을 비교하도록 한다.
- luminance masking : 밝은 영역에서 이미지 왜곡이 덜 보이는 현상
- contrast masking : 이미지내에 강렬한 activity나 texture가 있다면 이미지 왜곡이 덜 보이는 현상
- structure : 픽셀들이 공간적으로 가까이 있다면 강한 내부 의존성을 지닌다는 것
$$
SSIM(x, y) = [l(x,y]^{\alpha}] \cdot [c(x,y)]^{\beta} \cdot [s(x,y)]^{\gamma} \\
= \frac{(2\mu_x\mu_y + C_1)(2\sigma_xy + C_2)}{(\mu_x^2 + \mu_y^2 + C_1)(\sigma_x^2 + \sigma_y^2 + C_2)} \\

\sigma_{I\hat{I}} : \text{covariance} \\
C_1, C_2 : \text{constant for avoiding instability}
$$

$\alpha, \beta, \gamma$는 각각 상대적 중요도를 뜻하는데 만약 $\alpha=\beta=\gamma=1$ 이고 $C_3 = C2/2$ 이면 두번째 식으로 전개가 가능하다. 




# Applications


생성모델도 데이터를 만들어서 뭔가를 할수도 있지만 생성된 모델 자체를 이용하는 경우도 있다

## Text-to-Image


- Imagen



## Object Detection

- DALL-E for Detection: Language-driven Compositional Image Synthesis for Object Detection, https://arxiv.org/vc/arxiv/papers/2206/2206.09592v2.pdf



## Anomaly detection
- 아무래도 분포를 학습하다 보니 기존의 분포와 다른 데이터라는 점을 확인하게끔 하여 이상현상임을 판단할 수도 있음
- [Autoencoding Under Normalization Constraints](https://arxiv.org/abs/2105.05735)
- 오토인코더를 이용해서 이상치 탐지

