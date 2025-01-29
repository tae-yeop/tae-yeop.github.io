---
title:  "애니메이션, 만화, 웹툰 생성 모델"
excerpt:  "2D 만화 이미지 생성"
categories: 
- Generative Model
- Animation

tags:
- Generative Model
- Stable Diffusion
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-13
---

애니메이션, 만화 주제에 생성 모델을 활용하는 사례들


# Colorization

## 관련 데이터셋
- 역시 연구를 위해선 구할 수 있는 데이터셋이 필요함
- 오픈소스로 구할 수 있는 데이터셋
AnimeDiffusion


### SketchDeco
- [SketchDeco: Decorating B&W Sketches with Colour](https://arxiv.org/pdf/2405.18716)
- https://github.com/CHAITron/sketchdeco-code



![Untitled](https://github.com/user-attachments/assets/99d673a5-052d-436d-b294-afc615596031)

- ControlNet +  SD v1.5 + BLIP-2 text prompt를 사용
- $z_s = \mathcal{E}_s(S) ; z_s \in \Bbb{R}^{h \times w \times d}$
- $S \in \Bbb{R}^{512 \times 512 \times 3}$, 인풋 스케치, $\mathcal{E}_s$  : 스케치 인코더
- 컬러 팔레트 $\mathcal{P}_{\mathcal{H}} = \{h \}$, h : hexadecimal colur code
- 두 가지 목적식
    - 스케치로 부터 identity and shape를 유지하는 이미지 $\mathcal{I}^G$를 만듬 : $id(\mathcal{I}^G) \approx id(S)$
    - 색상이 선명한 결과물을 만듬 : $colour(\mathcal{I}^G) \approx colour(\mathcal{P}_{\mathcal{H}})$
    -


# Color Extraction