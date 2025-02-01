

## 패턴 파악
데이터로 문제는 푸는건 어떤 전략일까?
- 패턴 파악 전략
경험과 직관이라는 데이터가 쌓이면 판단력이 생긴다

기계 학습은 패턴을 알게끔 하는 일반화된 함수를 통해 목표를 달성한다.
패턴이란 결국 함수의 일종으로 볼 수 있지 않을까

## 대리 함수(local approximator, surrogate)
- VAE의 Lower Bound
- Policy-based의 surrogate function
- 목표가 되는건 아니지만 그걸 했으면 목표에 가까이 도달할 수 있는 녀석을 가지고 놀자
- 직접 관심이 되는 대상을 노리기 보단 훤씬 안정적이고 계산하기 용이한 녀석을 다루는 것
- J 를 직접 최적화하기 어려우므로, 근사적(local approximator)인 손실 함수 
𝐿를 사용하여 최적화한다는 의미로 해석
$$
\argmax_{\theta} (\mathcal{L_{\theta}}) \quad s.t \enspace \mathcal{L} \leq J(\pi_{\theta}) : \text{local appoximators of} J
$$

