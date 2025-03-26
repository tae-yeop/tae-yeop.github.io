---
title:  "생성 모델 VAE"
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


핵심 철학 중 하나는 Latent variable modeling



# VAE

- - solid theoratical foundation
- modeling good loss function challenging → suboptimal

이름에 대해...
- `오토 인코더`이다 보니 오토 인코더랑 같은거 아니냐고 생각할 수 있지만 최종적인 아키텍처 형태는 AE와 유사지만 이론적 배경은 Variational bayesian과 graphical model, probabilistic modeling이다.



## [VQ-VAE, 2017-11](https://arxiv.org/abs/1711.00937)

Motivation
(1) 실세계에서 이산적인 형태로 카테고리화된 코드를 사용하는 경우가 많다
- DNA sequence : A,C,G,T
- 언어 알파벳 : A,B,C …