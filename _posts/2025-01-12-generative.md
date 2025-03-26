---
title:  "생성 모델"
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

# 생성 모델 정리하기
내가 딥러닝이란 학문에 큰 관심을 가지게 된 계기가 바로 생성 모델이었다.
우연히 티스토리 배너 광고에 Udacity Deep learning nano degree 코스가 나왔고
이를 계기로 좀 더 알아보니 GAN을 이용한 생성 모델로 MNIST 숫자들을 만드는 것이 나왔다.
뭔가를 만들어낸다는 것. 내가 꿈꿔오던 것인데 이를 인공지능을 통해 할 수 있다는것에 꽂히고
지금의 위치까지 오게 된 것 같다.


# 생성이란 뭘까?
생성 모델은 생성을 한다. 그럼 생성이라는게 뭔지 정리를 해보자
사전적 의미는 사물이 생겨나거나 성질이 새롭게 출현한다는 것인데 영단어로 보자면 “generative”이다. 이는 라틴어 “generativus”에서 왔다. 



이는 “creative, productive, or procreative.”라는 뜻이고 root가 되는 동사는 “generare”이다. 이는 “to beget, produce, or generate.”이라는 뜻이다.
명사 형태는 “generatio”이고 이는 "genus" or "gen-”라는 라틴어에서 기원한다. 이는 "birth," "descent," or "kind.”를 의미한다. 
이것만 보면 생성이라는 사전적 의미와 큰 차이가 없는데 생물시간에 바웠던 gene이라는 단어, 즉 유전자와 같이
생각해보면 무언가 생성되기 위해선 시발점이 존재해야한다. 생명체의 경우 유전자, DNA가 될 것이다.

그럼 사람들이 뭔가 만들어내는 활동은 어떻게 생각할 수 있을까?
- 그림 그리기 : 생각 혹은 인지하고 있는 구상이나 컨셉을 도면에 그리는 것
- 음악 작곡, 연주 : 생각 혹은 인지하는 구상이나 컨셉을 악보나 악기를 이용해서 표현하는 것
- 글쓰기 : 생각 혹은 인지하는 스토리와 컨셉을 언어를 통해 표현하는 것
- 요리 : 재료를 통해 음식을 만든다


생각해보면 사람만이 뭔가를 만드는게 아니다. 사람도 자연 혹은 신이 만든 산물아닌가?
- 날씨 발생 : 자연이 만드는 생성인데 물리, 생물학적 작용을 통해 현상이 발생



# 수학자들의 개념 빌리기
일단 뭘 해야할지는 대략 정해진거 같다. 생성을 일으키는 시발점이 되는 대상을 어떤 주체가 받아서 생성물을 만든다. 컴퓨터 공학적으로 보자면 인풋이 알고리즘에 들어가서 아웃풋을 낸다로 치환볼 수 있을 것이다.
이를 좀 더 엄밀히 정의하고자 한다면 수학적인 모델링을 해야할 것이다. 수학적 모델링을 적절히 잘 해둔다면
계산을 할 수 있고 계산을 할 수 있다는 것은 코딩을 통해 결과를 얻을 수도 있다는 뜻이지 않을까

자연스럽게 생각해볼 수 있는건 함수의 형태.
$$
f(\cdot)
$$

앞서 말한 생명체의 경우

확률 분포라는 개념을 도입하게 된다. 가만히 생각해보면 현재 수학자들이 표현한 다수의 대상을 표현하고 논리를 전개하는 개념이 확률 통계이다. (이외에도 행렬이나 행렬 개념을 결합한 Random matrix theory가 있지만)
예를 들어 전세계 사람들의 키라는 개념을 생각할 때 당연히 하나의 값만 존재하는게 아닌 것을 안다. 이 많은 값을 하나의 수학 언어로 표현한다면 $p(x)$ 이렇게 간편하게 표현할 수 있다. 
거기다가 추가적으로 해당 값이 미래에 잘 나올지 안나올지에 대한 추가적인 정보까지 커플링되어서 표현할 수 있으니 유용한 개념으로 쓰일 수 있같은 느낌이 팍팍 든다.

마더 네이처 혹은 신만이 이러한 $p(x)$를 정확히 안다고 하자. 이게 흔히 수학시간에 배웠던 모분포이다.
여기서 우리가 할 수 있는 것은 $p(x)$의 구성값이 되는 데이터를 열심히 수집해서 $p(x)$을 추정하는 것이다. 이때 우리가 수집한 데이터의 모음에 대한 확률 분포를 $p_{data}(x)$라고 표현할 수 있을 것이다.



수학적으로 볼 때 결국 확률 분포를 

# 대표적인 분류

|**Model Type**|**Learning Objective** | **Sampling** | **Probability Distribution Model** | **Tractability** | **Flexibility** |
|--------------|-----------------------|--------------|------------------------------------|------------------|------------------|
| **Autoregressive** | MLE on $p_{\theta}(x)$: $\max_{\theta} \sum_{i=1}^N \log p_{\theta}(x_i \mid x_1, \dots, x_{i-1})$ | $ x_i \sim p_{\theta}(x_i \mid x_1, \dots, x_{i-1})$ | $p_{\theta}(\mathbf{x}) = \prod_{i=1}^n p(x_i \mid x_1, \dots, x_{i-1})$                        | High             | Medium (Causal structure fixed distribution)  |
| **VAE**            | MLE with surrogate loss (ELBO): $\max_{\theta} \mathbb{E}_{q_{\phi}(z \mid x)}[\log p_{\theta}(x \mid z)] - D_{\mathrm{KL}}(q_{\phi}(z \mid x) \mid p(z))$  | $ z \sim p(z), x \sim p_{\theta}(x \mid z) $   | $ p_{\theta}(x) = \int p(z) p_{\theta}(x \mid z) \, dz $                                          | Medium           | Medium (Dimension reduction fixed distribution, surrogate losses for intractable partition functions) |
| **Flow-based**     | MLE: $ \max_{\theta} \sum_{i=1}^N \log p_{\theta}(x_i) = \sum_{i=1}^N \log p(z_i) + \log \mid \det J_{f_\theta}(x_i) \mid  $                                        | $ z \sim p(z), x = f_{\theta}^{-1}(z) $   | $p_{\theta}(x) = p(z) \mid \det(J_{f_\theta}(x)) \mid = p(z) \mid \det\left(\frac{dz}{dx}\right) \mid $                           | High             | High (Invertible structure fixed distribution) |
| **Energy-based**   | MLE with minimizing energy function: $ \max_{\theta} \mathbb{E}_{x \sim p_{\text{data}}} \big[\log \frac{\exp(-E_{\theta}(x))}{Z(\theta)} \big] $         | $ x^{(t+1)} = x^{(t)} + \frac{\eta}{2} \nabla_x \log p_{\theta}(x^{(t)}) + \epsilon, \epsilon \sim \mathcal{N}(0, \eta) $ | $ p_{\theta}(x) = \frac{\exp(-E_{\theta}(x))}{Z(\theta)} $      | Low              | Very High (Surrogate losses for intractable partition functions) |
| **GAN**            | Implicit likelihood: $ \min_G \max_D \mathbb{E}_{x \sim p_{\text{data}}(x)}[\log D(x)] + \mathbb{E}_{z \sim p(z)}[\log (1 - D(G(z)))] $          | $z \sim p(z), x = G_{\theta}(z) $   | \( - \)   | High      | High               |
| **Diffusion**      | MLE on reverse process: $ \max_{\theta} \mathbb{E}_{q(x_{0:T})}[\log p_{\theta}(x_{0:T})] $,  $ q(x_{0:T}) $ :확산 과정을 통한 데이터의 조건부 분포 | $ x_T \sim \mathcal{N}(0, I), x_{t-1} = f_{\theta}(x_t, t) $ | $p(x_{0:T}) = p(x_T) \prod_{t=1}^{T} p_{\theta}(x_{t-1} \mid x_t) $        | Low     | Very High        |




## Autoregressive




# 왜 가우시안일까?
초기값이 되는 `z`로 보통 가우시안 분포에서 온 것으로 상정한다. GAN, VAE, Diffusion이던지 $z$를 모델에 넣어 $\hat{x}$를 만들고자 한다.
결국 학습할 데이터를 $z$에 잘 매핑시키고 나중에 $z$를 샘플링해서 사용하는건데 왜 굳이 가우시안일까? 그리고 가우시안 분포에 데이터를 매핑한게 실제 데이터 분포 $p_{data}(\cdot)$를 만들었다는 것은 어떻게 보장할까? 알고 보면 가우시안이 아닌 다른 분포에 매핑한게 더 좋을수도 있지 않을까?

먼저 보장한다는 것은 개별적인 프레임워크를 세부적으로 살펴보면서 보기로 한다. 여기선 가우시안을 쓰는 당위성에 대해 이야기해보기로 한다.

먼저 수학적으로 용이성이 있다. 
analytic하게 계산할 수 있는 부분이 많고 이는 pdf가 exp함수 그리고 이차식으로 구성되었다는 점에서 기인한다. 


다른 분포를 사용해볼 수도 있을까? [Non Gaussian Denoising Diffusion Models](https://arxiv.org/abs/2106.07582) 연구에선 감마분포와 mixtures of Gaussians을 사용했더니 성능 향상이 있음을 보였다. 취지는 가우시안 노이즈가 복잡한 데이터 분포를 캡쳐하지 못할 수도 있다는 것이다. DDPM 기준으로 생각해보면 파라미터 $\mu$를 학습하는 것인데 이 하나의 파라미터만으로는 완벽하게 데이터분포의 복잡도를 반영하기 힘들다는 것이다. 실제로도 DDPM이 잘 동작하려면 몇 가지 가정이 필요한데 여기서 자유도가 제약되는 점이 있다. 

감마분포와 mixtures of Gaussians를 사용한 이유는 자유도를 추가하면서도 기존 가우시안의 closed-form을 제공하듯이 마찬가지로 closed-form을 만들수 있어서 training and inference processes 포뮬레이션하기 쉽다는 점이다.




## 연도별 
- 2013
    - VAE
    - Denosing score matching
    - EBM



# 관련 자료
[스탠포드 CS236 생성모델 강의 자료](https://github.com/Subhajit135/CS236_DGM)
- 문제, 과제도 같이 있음

[기하학과 생성 모델 COMP760](https://joeybose.github.io/Blog/GenCourse)
- 복잡한 기하 구조를 가진 데이터에 대한 생성 모델

[Deep Generative Modeling](https://github.com/jmtomczak/intro_dgm)
- 책에 설명한 모델 구현 코드 레포

