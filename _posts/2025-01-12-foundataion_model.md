---
title:  "Foundation Model"
excerpt:  "파운데이션 모델"
categories: 
- Foundation Model

tags:
- Foundation Model
 
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-12
---

https://github.com/facebookresearch/sapiens?tab=readme-ov-file


# 비전 파운데이션 모델


## DINO
- 임베딩을 뽑으면 전반적으로 sparse and noisy correspondence field를 만든다

## DINOv2
- DINOv1에 스케일업한 버전 (더 큰 모델 + 더 정제한 대량 데이터)

# 파운데이션 모델 활용 예시

- 일종의 임베딩 추출기로 사용할 수 있다.
- 이런 파운데이션 모델들의 능력은 여러 논문에서 확인된 바 있음

- 특히 Semnatic correspondence을 잘 잡아냄
    - 다른 외형, 뷰포인트, non-rigide deformation을 가지는 같은 클래스에 속한 물체들의 dense correspondence를 예측하는 것

- 관련 내용 몇 가지 소개하면


## (21.12) [DINO-VIT-Features](https://dino-vit-features.github.io/)
- https://github.com/ShirAmir/dino-vit-features

- DINOv1이 효과적인 dense visual descriptor로 쓸 수 있다는 것을 보여줌
- 초반 레이어의 the “key” facet을 이용


## (23.05) [SD Complements DINO](https://sd-complements-dino.github.io/)
- https://github.com/Junyi42/sd-dino

<details>
  <summary>환경 구축</summary>
  
  ```python
    pip install loguru>=0.5.3
    pip install faiss-cpu>=1.7.1
    pip install matplotlib>=3.4.2
    pip install tqdm>=4.61.2
    pip install numpy>=1.21.0
    pip install gdown>=3.13.0

    pip install loguru faiss-cpu gdown 
    pip install -e ./sd-dino/third_party/Mask2Former 
    pip install -e ./sd-dino/third_party/ODISE
    pip uninstall detectron2 # https://github.com/facebookresearch/detectron2/issues/5010
    python3 -m pip install -U 'git+https://github.com/facebookresearch/detectron2.git@ff53992b1985b63bd3262b5a36167098e3dada02'
  ```

</details>

### SD features
![Image](https://github.com/user-attachments/assets/e8724f5c-9b3e-4365-b021-fc979ac7995d)
- Plug-and-play 연구에선 UNet의 feature가 I2I translation이 도움이 되는걸 보여준다
- UNet 디코더의 featuer를 뽑아봄 => 초반 layer엔 semantics와 structures, 후반엔 textures

![Image](https://github.com/user-attachments/assets/8ad479e6-c74d-49c8-ae85-babce12c0092)

- SD 1.5 UNet 디코더 2번,5번,8번 레이어의 feature를 같이 concat하여 사용 (timestep 100, implicit captioner)
- 그냥 채널 방향 concat -> 너무 큼 (1280 + 960 + 480 = 2720)
- 소스와 타겟 이미지의 i 번쨰 레이어 feature를 얻음 : $f_i^s, f_i^t$
- 둘을 cocat하고 PCA를 돌림
- 디코더에는 실제로 인코더에서 온 skip connection도 받는데 실험을 해보니 그냥 디코더 feature만 사용하는게 더 좋았다. 

![Image](https://github.com/user-attachments/assets/6bb60643-15c6-4c5b-a7a9-05d9f38a6a01)

### DINO features
![Image](https://github.com/user-attachments/assets/c54c39af-bc9a-4441-ad16-30f372d3804b)
- DINOv2 feature는 11레이어(마지막 레이어)의 toke facet를 얻음


![Image](https://github.com/user-attachments/assets/cba5b12c-d6f2-4e16-bd0c-59a849731bb7)

![Image](https://github.com/user-attachments/assets/0059ddc7-befe-42f0-b41b-b6b655e6b868)

![Image](https://github.com/user-attachments/assets/55dee9b0-f788-49a6-8729-e1fb9662dc91)

![Image](https://github.com/user-attachments/assets/d57f82a1-d62c-4c59-86d4-645399de4ae4)

![Image](https://github.com/user-attachments/assets/6703a235-d117-4a13-999f-b6c820e910e4)

![Image](https://github.com/user-attachments/assets/1ab1e0c2-860b-4054-a6be-394ca1dd883e)

![Image](https://github.com/user-attachments/assets/9f1fa881-66fd-42f5-a7f2-3da119997e44)







## [LUMEN](https://openreview.net/pdf?id=zPg9JdIUOJ)
- SD 모델에 Semantic segmenation 정보와 여기에 풍부한 semantic과 geometric layout 정보가 있다는 걸 활용한 연구
- 기존의 컨디션 정보는 부족함이 있음
    - Semantic segmenation : do not contain full information about the object pose, orientation, or geometry
    - Edge, Depth : limited spatial information and are ambiguous in terms of the object semantics ⇒ 이것만으로 cat인지 blanket인지 구분이 힘들다 ⇒ 잘못된 구분을 할 수 있다
![Image](https://github.com/user-attachments/assets/4136f6d3-296d-4df4-b647-87fa100b3510)
- (1) SD UNet의 2,5,8번 레이어에서 activation을 뽑고 8번 레이어 사이즈에 맞춰 업샘플링
- (2) 채널 방향으로 concat
- (3) PCA를 수행해서 linear projection
- (3)-(1) 먼저 학습 데이터셋에서 40K개의 피처 벡터를 뽑고 N=20 짜리 PCA를 돌려놓음
- (3)-(2) 이를 통해 20개의 PCA compoennts를 사용함
- (4) 앞에서 만든 Neural layout을 ControlNet에 넣음

![Image](https://github.com/user-attachments/assets/017e489f-1e38-4f86-bfba-caf9c55a45d1)
- DINO, DINOv2, CLIP, and SD features를 통해 이미지 생성했을 시 평가
- CLIP이 다양한 이미지를 만들긴 함 ⇒ 이는 weak semantic + spatial constraints 때문
- CLIP is trained with an image-level objective, it is less suitable to capture precise pixel-level information without further processing

![Image](https://github.com/user-attachments/assets/a3cf5484-2405-4404-92ab-82005a54e7e4)
- Neural Layout을 제외한 다른 경우는 ⇒ limited spatial information and are semantically ambiguous.

![Image](https://github.com/user-attachments/assets/3199aa69-fb61-47e9-b793-b7e6a2242ce0)

![Image](https://github.com/user-attachments/assets/b8917530-bb5d-40a0-8dac-56d13e442b2f)
- out-of-distribution prompt edits도 수행 가능
- Image manipulation through prompt editing on the COCO-Stuff validation set. Sample은 prompt 수정없는 그대로 버전

![Image](https://github.com/user-attachments/assets/80db71b8-86e0-41ea-80a4-9501157f6468)
- Training Data for Multiple Tasks
- 만들어진 데이터셋으로 다른 downstream task 모델을 학습시켜봄
- SegFormer와 TaskPrompter을 학습
![Image](https://github.com/user-attachments/assets/eea8dcc9-c115-4731-becb-592f79911e7d)
- prompt를 domain을 컨트롤 (appearance)
- neural layout를 사용 ⇒ semantic and geometric content.