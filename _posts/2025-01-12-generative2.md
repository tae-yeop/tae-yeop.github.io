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
- 


# 평가 메트릭
애매한 부분에 왔다. classification model의 경우 정확도, FPR 등 정확히 딱 계산되는 평가 메트릭이 있는데 아쉽게도 generative model에선 우리가 인지하는 것과 상반되는 것을 보여주기 때문이다.




# Applications
- 생성모델도 데이터를 만들어서 뭔가를 할수도 있지만 생성된 모델 자체를 이용하는 경우도 있다
## Object Detection

- DALL-E for Detection: Language-driven Compositional Image Synthesis for Object Detection, https://arxiv.org/vc/arxiv/papers/2206/2206.09592v2.pdf



## Anomaly detection
- 아무래도 분포를 학습하다 보니 기존의 분포와 다른 데이터라는 점을 확인하게끔 하여 이상현상임을 판단할 수도 있음
- [Autoencoding Under Normalization Constraints](https://arxiv.org/abs/2105.05735)
- 오토인코더를 이용해서 이상치 탐지

