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
뭔가를 만들어낸다는 것. 내가 꿈꿔오던 것인데 이를 인공지능을 통해 할 수 있다는것에 큰 매력이 느껴게 되었고 그 때부터 


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



수학적으로 볼 때 결국 확률 분포를 그런데 근사화한다. 이를 likelihood를 최대화한다고 말한다.

![Image](https://github.com/user-attachments/assets/1ca8befe-30f8-4ae5-b579-baae3ca8221b)


그런데 이러한 f는 분명 복잡할 텐데 컴퓨터 프로그램상으로 이 f를 표현할 수 있을까? 직접적으로 f를 표현하는게 쉽지 않다. 대신에 우리는 결과물과 재료가 무엇인지 알고 있다면 데이터를 모아서 data-driven approach를 취할 수 있지 않을까?


통계적 학습법으로 관점을 바꾸도록 하자. 아프리카 Himba 부족들은 녹색과 파란색을 구분하는 단어가 없다고 한다. 이들은 녹색과 파란색을 표현하는데 제한이 되는 것이다. 수학도 일종의 언어로 바라 볼 수 있는데 통계라는 수학적 언어를 이용하면 더욱 잘 표현할 수 있게 된다. 루트비히 비트겐슈타인의 "논리철학 논고"에 실린 "내 언어의 한계는 내 세계의 한계이다"라는 명언을 간결하게 표현

통계적으로 표현하기 위해선 확률과 통계의 언어를 배워야한다

확률이란 무엇인가?
15세기 르네상스 시기, 루카 파치올리(회계학의 아버지)의 저서 <산수, 기하학, 비례와 비례적인 것들의 대전>에서 점수의 문제(Problems of Points)를 언급한다. 

두 참가자가 1만원씩 모아서 판돈 2만원을 만들고 점수를 얻는 게임을 하여서 도박을 한다. 게임은 간단히 주사위를 던져서 높은 수가 나오는 사람이 점수를 얻는다고 하자. 먼저 목표 점수에 도달한 사람이 모든 돈을 갖게되는데 이때 갑자기 게임이 중단되면 판돈을 어떻게 나눌지 고민

만약 A가 더 많은 점수를 가지고 있고 B가 더 적은 점수를 가질시 A가 모두 가져야할까? 끝까지 가면 모를수도 있다.
루카 파치올리는 점수비율로 판돈을 나누는게 합리적이라고 보았다.

16세기 중반 니콜로 타르탈리아는 여기에 문제를 제기하였다. 목표점수가 100점인데 A가 99점이고 B가 50점인 상황에서 A가 거의 이긴것과 다름없다. 만약 1점 vs 0점인 상황이면 누가 이길지 예측하기 어렵지만 1점을 차지했다고 해서 판돈을 모두 획득하는 건 말이 되지 않는다. 그는 답을 찾을 수 없는 문제라고 보았다.

시간이 흘러 페르마와 파스칼는 이 문제에 대해 논의하게 된다.
핵심은 A와 B가 이길 확률이 무엇이냐는 것이었다. 지금까지 딴 점수가 문제가 아니라 앞으로 딸 점수가 어떻게 될 것이냐는 것

즉 과거가 아닌 미래에 대한 생각이다. 다시 말해 미래에 일어날 일을 기술하는 것이 확률이다.페르마와 파스칼은 중단 지점에서 각 플레이어의 승리 확률을 계산하고 여기에 기대값으로 계산하여 돈을 나눠줘야한다고 생각했다. 

이때 확률을 계산하기 위해 먼저 갖춰야 할것은 확률 모델이다. 앞의 예에서 주사위를 던지는데 공정한 주사위라면 균등한 확률 모델이 될 것이다. 이 확률 모델을 기초로 확률을 얻고 기대값을 얻고 앞으로 미래 사건을 예측한다. 

그럼 통계는 무엇일까? 통계는 출발점이 데이터이다. 데이터를 통해 확률 모델을 찾고 해석을 한다. 이런 데이터를 보았을 때 어떤 모델이 맞을지를 확인하고 모델을 얻었다고 생각하면 다시 우리는 확률과 기대값을 얻을 수 있다. 


```python
import random

def roll_dice():
    i = random.uniform(0, 1)
    if i <= 1/6:
        print('1')
    elif i <= 2/6:
        print('2')
    elif i <= 3/6:
        print('3')
    elif i <= 4/6:
        print('4')
    elif i <= 5/6:
        print('5')
    elif i <= 6/6:
        print('6')

```

이제 딱딱한 텍스트북 형태로 생성모델이 뭔지 정리하면 다음과 같다. 

> A generative model takes a training set with samples drawn from some distribution $p_{data}$ and learns to represent an estimate $p_{model}$ of that data-generating distribution.


# 생성 모델의 중요성?

리처드 파인만은 다음과 



# 인공신경망으로 구현하기
실제 neural net으로 표현을 하게 되면 $f(\cdot, \theta)$으로 표현하게 된다. 이는 이론을 전개할 때 사용한 $P_\theta$가 아니다. 하지만 $P_{\theta}$처럼 생각할 수 있다. 왜냐면 f에서 계속해서 샘플링을 하면 결국 분포를 만들 수 있고 이 분포를 $P_{\theta}$라고 취급할 수 있다. 

즉, $\theta$에 분포에 대한 정보가 녹아 있다고 할 수 있다.






# 생성 모델을 얻는 과정

## (1) 분포를 먼저 학습한다

분포를 학습한다는 것은 데이터가 실현된 분포 $p_{data}(x)$를 학습한다는 것을 말한다. 

주집한 데이터들이 어떠한 분포에서 샘플되었다고 가정한다.

만약 이 분포를 찾아낼 수 있다면 관심을 가지는 데이터를 새롭게 만들 수 있다

물론 100프로 똑같은건 찾아낸다는 건 상식적으로 생각해도 말이 안되는거지만 대충 근사적인 분포까지만 찾아낼 수 있다면 여기서 샘플링하면 내가 모은 데이터와 비슷한 데이터를 만들어 낼 수 있을 것이다. 

모델 분포 $p_{\theta}(x)$가 $\theta$을 이용해서 만들 수 있다고 상정하고 $p_{data}(x)$에 대해 density estimation을 하게 된다.


이는 MLE를 통해 수행할 수 있다. 이때 확보한 데이터끼리 IID를 가정하여 동일한 marginal $p_{data}(x)$를 여러번 곱하여 Joint distribution을 구성한다고 상정한다.


이론적으론 well-posed이지만 실제론 ill-posed 이다.
데이터 희소성





## (2) 샘플링 한다

Discriminative Model 혹은 Statistical Modeling에선 Inference라고 부른다. Discriminative Model에선 observation x 에서 z를 얻기 때문
- 반면에 Generative Model에선 z에서 x를 얻도록 한다.


![Image](https://github.com/user-attachments/assets/12e8a0e6-b9cf-48d6-bcf4-15a812ba7965)

![Image](https://github.com/user-attachments/assets/cbc53e24-8ef2-4eed-9204-e5c3ae76c9ad)






### 샘플링에서 이슈 사항

샘플링을 해보면 문제가 되는 경우가 있다

support 부근의 데이터만 뽑아내거나 diverse한 이미지를 만들지 못하는 경우

보통 이런 이슈는 diversity vs quality 문제로 연관된다

또한 학습할 때 Conditional Generation 형태로 학습했다면 Condition 정보를 보다 자세한것을 주면 퀄리티가 높아질 것을 기대할 수 있다. 예를 들어 text conditon의 경우 ⇒ CLIP이 broad한 단어로 구성되어 있어서 그럴 수도

좀 더 디테일한 텍스트일수록 자세하고 고정적으로 나와야할것 같고

broad general할 수 록 다양하게 나와얗ㄹ거 ㅅ같고

관련된 연구들

Diversity Balancing Generative Adversarial Networks for fast simulation of the Zero Degree Calorimeter in the ALICE experiment at CERN


Diverse Diffusion: Enhancing Image Diversity in Text-to-Image Generation

Class-Balancing Diffusion Models

CADS: UNLEASHING THE DIVERSITY OF DIFFUSION MODELS THROUGH CONDITION-ANNEALED SAMPLING


## (3) 응용 : 컨트롤하자


# 대표적인 분류

|**Model Type**|**Learning Objective** | **Sampling** | **Probability Distribution Model** | **Tractability** | **Flexibility** |
|--------------|-----------------------|--------------|------------------------------------|------------------|------------------|
| **Autoregressive** | MLE on $p_{\theta}(x)$: $\max_{\theta} \sum_{i=1}^N \log p_{\theta}(x_i \mid x_1, \dots, x_{i-1})$ | $ x_i \sim p_{\theta}(x_i \mid x_1, \dots, x_{i-1})$ | $p_{\theta}(\mathbf{x}) = \prod_{i=1}^n p(x_i \mid x_1, \dots, x_{i-1})$                        | High             | Medium (Causal structure fixed distribution)  |
| **VAE**            | MLE with surrogate loss (ELBO): $\max_{\theta} \mathbb{E}_{q_{\phi}(z \mid x)}[\log p_{\theta}(x \mid z)] - D_{\mathrm{KL}}(q_{\phi}(z \mid x) \mid p(z))$  | $ z \sim p(z), x \sim p_{\theta}(x \mid z) $   | $ p_{\theta}(x) = \int p(z) p_{\theta}(x \mid z) \, dz $                                          | Medium           | Medium (Dimension reduction fixed distribution, surrogate losses for intractable partition functions) |
| **Flow-based**     | MLE: $ \max_{\theta} \sum_{i=1}^N \log p_{\theta}(x_i) = \sum_{i=1}^N \log p(z_i) + \log \mid \det J_{f_\theta}(x_i) \mid  $                                        | $ z \sim p(z), x = f_{\theta}^{-1}(z) $   | $p_{\theta}(x) = p(z) \mid \det(J_{f_\theta}(x)) \mid = p(z) \mid \det\left(\frac{dz}{dx}\right) \mid $                           | High             | High (Invertible structure fixed distribution) |
| **Energy-based**   | MLE with minimizing energy function: $ \max_{\theta} \mathbb{E}_{x \sim p_{\text{data}}} \big[\log \frac{\exp(-E_{\theta}(x))}{Z(\theta)} \big] $         | $ x^{(t+1)} = x^{(t)} + \frac{\eta}{2} \nabla_x \log p_{\theta}(x^{(t)}) + \epsilon, \epsilon \sim \mathcal{N}(0, \eta) $ | $ p_{\theta}(x) = \frac{\exp(-E_{\theta}(x))}{Z(\theta)} $      | Low              | Very High (Surrogate losses for intractable partition functions) |
| **GAN**            | Implicit likelihood: $ \min_G \max_D \mathbb{E}_{x \sim p_{\text{data}}(x)}[\log D(x)] + \mathbb{E}_{z \sim p(z)}[\log (1 - D(G(z)))] $          | $z \sim p(z), x = G_{\theta}(z) $   | \( - \)   | High      | High               |
| **Diffusion**      | MLE on reverse process: $ \max_{\theta} \mathbb{E}_{q(x_{0:T})}[\log p_{\theta}(x_{0:T})] $,  $ q(x_{0:T}) $ :확산 과정을 통한 데이터의 조건부 분포 | $ x_T \sim \mathcal{N}(0, I), x_{t-1} = f_{\theta}(x_t, t) $ | $p(x_{0:T}) = p(x_T) \prod_{t=1}^{T} p_{\theta}(x_{t-1} \mid x_t) $        | Low     | Very High        |

모델 패밀리별 알아두어야 할 사항

(1) **Probability Distribution Model**

Generative Model $p_{\theta}(x)$를 어떻게 디자인할지는 연구자가 설정하는 부분이다. 파라미터 $\theta$를 어떻게든 찾아서 진정한 $p_{data}(x)$에 근사되기를 기대하면서 모델링하게 되는데 각각의 접근법마다 나름의 근거와 철학이 있다. 다시 말해 앞서 설명했듯이 공통의 목표는 “모델을 통해 데이터 분포를 근사한 분포를 얻고 여기서 샘플링하기” 였는데 목표는 같더라도 다양한 접근법이 제시되었다.2025년 현재시점에선 Diffusion model의 접근법이 가장 인정받는 방식이다(나중에 또 시간이 흐르면 더 좋은 방식을 찾을 수 있을지도 모르지만).

확실한건 다이렉트로 $p_{\theta}(x)$를 계산하는게 힘든 경우가 대부분이다 ⇒ intractible

그래서 이를 해결하는 방식으로 연구가 진행되었고 이는 개별적인 모델 프레임워크로 분화되었다.

(2) **Learning Objective**

Generative Model을 얻고자 한다는 것은 high-dimensional data distribution $p_{data}(x)$를 모델링하는 것이 목표이다. Statistical Learning의 관점으로 보자면 $p_{data}(x)$에 대한 Densitiy estimation을 수행이 필요하다. 특히 Parameter estimation을 통해 수행해야 한다.

$$
p(x_1, x_2, \dots , x_n) = \prod_{i=1}^{n} p_{data}(x_i)
$$

결국 수집한 데이터셋 분포와 모델의 분포를 최소화하는 것이다. 모두 근본적으로 maximum likelihood에서 출처를 하고 있음

$$
\Large \hat{\theta} = \argmax_{\theta} \Bbb{E}_{x \sim P_{data}}[\log{P_{\theta}(x)}]
$$

이때 MLE 수식을 잘 정리하면 다음과 같은 최적화 식을 얻을 수 있고 이를 딥러닝 모델의 목적식으로 사용하게 된다.

$$
\theta^* = \argmin_{\theta} D_{KL} (p_{data}(x) || p_{\theta}(x))
$$

(3) **Sampling**

학습하고 나면 얻게 되는 모델을 어떻게 샘플링할지도 고민사항이다. 이는 위에서 Probability Distribution Model을 어떻게 셋업하느냐에서 기인한다. 빨리 뽑을 수 있는지를 가지고 `Sampling Efficiency`를 논하게 된다.

- Latent Variable Model의 경우 $z \sim p(z)$를 뽑고 나서 이를 인풋으로 넣어서 생성
- Diffusion model의 경우 $x_T \to x_{T-1} \to \cdots \to x_0 $으로 여러 번 Evaluation을 통해 샘플하게 된다

(4) Flexibility (Sohl-Dickstein et al.,에 언급된 설명)

- 모델이 flexible하다는 것 ⇒ 다양한 형태의 데이터 분포를 잘 모델링할 수 있고 자유롭게 아키텍처를 설계할 수 있다
- 모델이 flexible하지못한 것 ⇒ 모델이 특정한 achitecture 혹은 특정한 distrbution으로 고정


- AR: 중간. 데이터를 조건부로 모델링, Causality를 가정할 수 있는 순차적인 데이터 유형(예: 이미지)에 제한된다
- VAE(RBM) : 중간. latent space의 구조에 제한받는다
- Flow-based : 높음. Invertible function이어야 하고 고차원 데이터에 대해 계산 복잡성이 낮아야 한다
- Energy-based : 매우 높음. 특정한 아키텍처에 제한받지 않음.
- GAN : 높음. 학습 과정의 안정성 문제가 제약을 줄 수 있음
- Diffusion : 매우 높음. 특정한 아키텍처에 제한받지 않음

(5) Likelihood Computation
- Tractable한 모델은 closed form으로 analyticall evaluation을 할 수 있다.
- 예를 들어 가우시안과 같이 우리가 잘 아는 분포 모델로 likelihood 등의 계산을 수행할 수 있다.
- 이게 좋은 이유는 likelihood를 통한 비교를 통해 성능 분석을 할 수 있다.
- AR : 높음. 각 차원의 데이터를 조건부 확률로 모델링 ⇒ 대부분 분석적으로 전체 likelihood를 직접 계산 가능
- VAE : 중간. ELBO를 사용하여 likelihood를 근사 ⇒ ELBO는 분석적으로 계산 가능 + 전체 모델의 likelihood는 closed form으로 표현되지 않음
- Flow-based : 높음. 가역적인 변환을 사용하여 데이터의 분포를 정확하게 모델링하고, likelihood는 closed form으로 계산
- Energy-based : 낮음. $Z(\theta)$를 계산하는게 일반적으로 불가능 ⇒ likelihood는 closed form으로 표현되지 않음 ⇒ MCMC,  Contrastive Divergence을 통한 근사적 계산
- GAN : X, Likelihood can’t be evaluated
- Diffusion : 낮음. 근사적인 방법으로 계산


(6) Latent Representation and Control
- **Autoregressive Models :** 각 차원을 순차적으로 생성 ⇒ 단계마다 모델이 무엇을 하는지 이해하기쉽다
- **VAE : latent space 통해 해석할 수 있다**
- **Flow-based Models : 가역적인 변환으로 무슨일이 일어나느지 추적할 수 있다**
- **EBM** : 에너지 함수의 복잡성으로 인해 내부 매커니즘 해석이 어렵다
- **GAN** : 특정한 구조를 강제화(StyleGAN)시켜야 한다
- **Diffusion** : 각 단계를 latent space 처럼 생각할 수 있다

## Autoregressive

$$
p_{\theta}(\mathbf{x}) = \prod_{i=1}^n p(x_i | x_1, ..., x_{i-1})
$$

<img src="https://github.com/user-attachments/assets/6c575ffb-99bb-42c2-8f1d-5b73dad65faf" width="400"/>



LLM의 핵심 동작 방식

자연어가 아닌 다른 도메인에선 상대적으로 인기가 없음

이미지 생성의 경우 픽셀 단위로 하면 비용이 너무 큼

그래서  vector-quantized tokens을 이용하느 경향이 잇음







## VAE(RBM)

$$
p_{\theta}(x) = \int p(z) p_{\theta}(x|z) dz \\

\max_{\theta, \phi} {\Bbb{E}{z \sim q_{\phi}(\mathbf{z}|\mathbf{x})}[p_{\theta}(\mathbf{x}|\mathbf{z})]} - KL(q_{\phi}(\mathbf{z}|\mathbf{x}) || p_{\theta}(\mathbf{z}))
$$


## Energy-based Model

$$
\max_{\theta} \Bbb{E}_{x \sim p_{data}}[\log{p_{\theta}(x)}] \\
= \max_{\theta} \Bbb{E}_{x \sim p_{data}} [log \frac{\exp(-E_{\theta}(x))}{Z(\theta)}] \\
= \max_{\theta} \Bbb{E}_{x \sim p_{data}} [-E_{\theta}(x)] \\
= \min_{\theta} \Bbb{E}_{x \sim p_{data}} [E_{\theta}(x)]
$$

![Image](https://github.com/user-attachments/assets/eaf582fe-0adc-4e6a-9c35-6d9f6903e71d)

## GAN

$$
\max_{\theta_D} \min_{\theta_G}\Bbb{E}_{x\sim p_{\text{data}}}[log(D(x))] + \Bbb{E}_{z \sim p(z)} [log(1-D(G(z)))]
$$

<img src="https://github.com/user-attachments/assets/6aa8af0c-31fc-4b98-90c6-84a5973c66b9" width="400"/>

- known for potentially unstable training and less diversity in generation due to their adversarial training nature
- 복잡한 분포의 샘플링 과정을 모델링한다.


## Diffusion model

<img src="https://github.com/user-attachments/assets/a0fbeeda-f953-4da5-8ec6-47e3fcc273f4" width="400"/>


Gradullay add gaussian noise and then reveser.

Unlike VAE or flow models, diffusion models are learned with a fixed procedure and the latent variable has high dimensionality (same as the original data)



용어 정리 : Implicit Density Models vs Explicit Density Models
![Image](https://github.com/user-attachments/assets/fd2fea9e-1356-4886-ae33-e52598cd2462)
(1) Implicit Density Models

직접적으로 likelihood에서 유도된 식을 최대화시키지 않는다. 즉 네트워크의 생성 결과와 데이터를 직접 비교하는 방식이 아니라 보조적인 방식을 사용한다. 예를 들어 Moment Matching의 경우 데이터의 통계적 속성(예: 평균, 분산)을 매칭하는 방식으로 샘플을 생성한다. 이를 통해 데이터 분포의 likelihood를 간접적으로 최대화한다. 학습을 위한 수식을 유도하는 과정에서 직접적으로 likelihood에서 시작하지 않는다

(2) Explicit Density Models
여기선 학습 식을 유도할 때 likelihood을 직접적으로 사용하게 된다. likelihood-based model이라고도 한다. 한 번 더 세부적으로 분류한다면 관심을 가지는 데이터 분포에 대한 density를 정확히 계산이 가능한지 아닌지에 따라 접근법을 달리 할 수 있는다 (Tractable denstiy vs Non-tractable denstiy) 정확히 계산이 불가능하다면 근사화된 방식을 취하도록 한다. 즉 likelihood 식에선 probability density function를 사용해서 표현하는데 이 pdf를 사용했을 때 tractaibl하게 계산할 수 있는지 여부가 중요해진다. 수집한 데이터 샘플과 높은 likelihood를 내도록 모델을 학습하는 AR, NF 계열이 있고 likelihood를 직접 계산하지 못해 Variational Approximation이나 energy function optimization, score optimization을 취하기도 한다. energy function optimization은 energy function이라는 우회로를 사용한다. score-based는 energy function 자체를 학습하지 않고 energy-based model의 score를 학습하도록 한다. diffusion model은 likelihood-based와 score-based 해석 둘 다 가질 수 있다




# 왜 가우시안일까?
초기값이 되는 `z`로 보통 가우시안 분포에서 온 것으로 상정한다. GAN, VAE, Diffusion이던지 $z$를 모델에 넣어 $\hat{x}$를 만들고자 한다.
결국 학습할 데이터를 $z$에 잘 매핑시키고 나중에 $z$를 샘플링해서 사용하는건데 왜 굳이 가우시안일까? 그리고 가우시안 분포에 데이터를 매핑한게 실제 데이터 분포 $p_{data}(\cdot)$를 만들었다는 것은 어떻게 보장할까? 알고 보면 가우시안이 아닌 다른 분포에 매핑한게 더 좋을수도 있지 않을까?

먼저 보장한다는 것은 개별적인 프레임워크를 세부적으로 살펴보면서 보기로 한다. 여기선 가우시안을 쓰는 당위성에 대해 이야기해보기로 한다.

먼저 수학적으로 용이성이 있다. 
analytic하게 계산할 수 있는 부분이 많고 이는 pdf가 exp함수 그리고 이차식으로 구성되었다는 점에서 기인한다. 


다른 분포를 사용해볼 수도 있을까? [Non Gaussian Denoising Diffusion Models](https://arxiv.org/abs/2106.07582) 연구에선 감마분포와 mixtures of Gaussians을 사용했더니 성능 향상이 있음을 보였다. 취지는 가우시안 노이즈가 복잡한 데이터 분포를 캡쳐하지 못할 수도 있다는 것이다. DDPM 기준으로 생각해보면 파라미터 $\mu$를 학습하는 것인데 이 하나의 파라미터만으로는 완벽하게 데이터분포의 복잡도를 반영하기 힘들다는 것이다. 실제로도 DDPM이 잘 동작하려면 몇 가지 가정이 필요한데 여기서 자유도가 제약되는 점이 있다. 

감마분포와 mixtures of Gaussians를 사용한 이유는 자유도를 추가하면서도 기존 가우시안의 closed-form을 제공하듯이 마찬가지로 closed-form을 만들수 있어서 training and inference processes 포뮬레이션하기 쉽다는 점이다.


## 샘플링
들고 있는 데이터셋으로 최선을 다해 학습했었도 샘플링은 하는건 또 다른 영역이다.
support 부근의 데이터만 뽑아내거나 diverse한 이미지를 만들지 못하는 경우
이슈는 diversity vs quality의 문제


## 컨트롤
조건부 생성



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

