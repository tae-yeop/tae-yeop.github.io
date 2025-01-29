---
title:  "오픈소스 생성 모델"
excerpt:  "그 동안 공부해온 발자취"
categories: 
- Generative Model
- Huggingface

tags:
- Generative Model
- Huggingface
- Stable Diffusion
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-12
---

# 개요
- 대표적인 오픈소스 생성 모델 파운데이션 모델이자 SD에 대해 정리
- 아무래도 상업적으로 사용가능하기 때문에 저작권에 문제없이 이를 기초로 활용하기 좋다


원래 Stable Diffusion 자체는 LDM을 대규모 데이터셋(LAION)에 학습해서 가능성을 보여준것에
지나지 않았지만 더욱 대중들이 많이 접하게 되는 계기를 만들었고
펀딩이 잘되어서 그런지 후속 연구 결과로 나온 모델들도 성능이 대폭 향상되었다.
아무래도 이목이 집중되다 보니 저작권 이슈 등 여러가지 제약조건에도 직면하게 되었는데
특정 연예인 사진이나 특정 아티스트의 스타일을 못쓰게 되는 경우도 생김

이후 Stability의 SD 이후로 벤처나 엔비디아 혹은 중국 테크 기업 등에서 여러 생성용 파운데이션 모델을
오픈하였음

# 기본 비교

| 버전    | 데이터셋    | 학습 방법  | UNet   | 주요 특징        |
|--------|-------------|---------------|---------------------|----------------------------|
| Stable Diffusion v1.5 | LAION-5B                   | 텍스트-이미지 쌍                     | Latent Diffusion Model (LDM), UNet, CLIP 텍스트 인코더 | 고차원 이미지 데이터를 저차원 라티스 공간에 매핑하여 연산 효율성 향상                       |
| Stable Diffusion v2.0 | LAION-Aesthetics v2        | 텍스트-이미지 쌍, 업데이트된 최적화 알고리즘과 정규화 기법 | Latent Diffusion Model (LDM) v2, 개선된 UNet, 업데이트된 CLIP 텍스트 인코더, 새로운 노이즈 스케줄링 기법 | 데이터 품질 향상 및 노이즈 스케줄링 기법 도입으로 성능 개선                                 |
| Stable Diffusion v2.1 | LAION-Aesthetics v2 (확장) | 더 많은 데이터와 높은 품질의 이미지, 최신 정규화 기법과 최적화 알고리즘 | Latent Diffusion Model (LDM) v2.1, 더욱 개선된 UNet, 최신 CLIP 텍스트 인코더, 효율적이고 정확한 라티스 공간 매핑, 최적화된 노이즈 스케줄링 기법, 하이퍼파라미터 튜닝 | 더욱 향상된 이미지 생성 품질과 텍스트-이미지 매핑 정확도                                     |
| Stable Diffusion v2.1-base | LAION-Aesthetics v2 (확장) | 더 적은 자원으로 빠른 학습과 추론       | Latent Diffusion Model (LDM) v2.1 (경량화), 경량화된 UNet, 최신 CLIP 텍스트 인코더 | 빠른 학습과 추론을 위한 경량화 버전                                                       |
| SDXL                  | 미공개 (프리미엄 데이터셋) | 고품질 데이터와 대규모 연산 자원을 활용한 학습 | Latent Diffusion Model (LDM) XL, 매우 개선된 UNet, 최신 CLIP 텍스트 인코더 | 최상의 이미지 생성 품질, 복잡한 장면과 스타일 생성 능력 향상                                |
| SDXL-lightning        | 미공개 (프리미엄 데이터셋) | 고품질 데이터, 최신 학습 기법 적용    | Latent Diffusion Model (LDM) XL (경량화), 매우 개선된 UNet (경량화), 최신 CLIP 텍스트 인코더 | SDXL의 경량화 버전으로, 빠른 연산과 메모리 효율성 제공                                     |




# 아키텍처
- v1 and v2 (i.e., v1.1/2/3/4/5, v2.0/1, and v2.0/1-base)간의 UNet의 아키텍처적인 차이는 없다
- 다이어그램은 [BK-SDM 논문](https://arxiv.org/pdf/2305.15798)에서 매우 깔끔하게 정리되어 있다

![Untitled](https://github.com/user-attachments/assets/6ea12390-1ebe-4965-afac-e173fde9a93f)

![Untitled](https://github.com/user-attachments/assets/3a015ebb-a25a-4fc9-aced-6d6556a86443)

![Untitled](https://github.com/user-attachments/assets/7074d0be-5e7a-4812-93bc-fd08db4605d0)

- 허깅 페이스 기준으로 보면 "DownBlock2D", "AttnDownBlock2D", "AttnDownBlock2D", "AttnDownBlock2D”
"AttnUpBlock2D", "AttnUpBlock2D", "AttnUpBlock2D", "UpBlock2D”


- SDXL은 뒤쪽에 Refiner를 둬서 SR을 할 수 있음



# Variants

## SDXL-Lightning
- 

## SD3-Turbo
- [LADD(Latent Adversarial Diffusion Distillation)](https://arxiv.org/abs/2403.12015)를 SD3에 적용
- 티처를 써서 합성데이터를 만들고 이 피처를 이용해 GAN loss를 적용

![image](https://github.com/user-attachments/assets/1163115c-3b22-44d1-96c5-589d9e4cd0eb)

## Flux
- 애초에 FLUX.1 [dev] 또한 FLUX.1 [pro]에서 guidance-distilled 시킨 모델임
- FLUX.1 [schnell]의 경우 adversarial diffusion distillation(ADD)을 적용하여 1~4스텝만에 뽑아냄

# 체크포인트
## SD v1.5

(1) [**stable-diffusion-v1-1**](https://huggingface.co/CompVis/stable-diffusion-v1-1)

- laion2B-en 데이터셋에 대해 256x256으로 237k steps 학습
- 이후 170M examples from LAION-5B with resolution >= 1024x1024 데이터셋에 대해 512x512로 만들어서 194k steps 파인튜닝

(2)[**stable-diffusion-v1-2**](https://huggingface.co/CompVis/stable-diffusion-v1-2) 

- 1.1 체크포인트에서 laion-improved-aesthetics" (a subset of laion2B-en) 데이터셋으로 515K steps 파인튜닝

(3) [**stable-diffusion-v1-5**](https://huggingface.co/runwayml/stable-diffusion-v1-5) (v1-5-pruned.ckpt)

- 1.2 체크포인트에서 laion-aesthetics v2 5+ 데이터셋의 512x512  해상도에 대해 595k steps 파인튜닝

(4) [**stable-diffusion-inpainting**](https://huggingface.co/runwayml/stable-diffusion-inpainting) (sd-v1-5-inpainting.ckpt)

- 1.2 체크포인트에서 595k steps만큼 학습 이후
- laion-aesthetics v2 5+에 대해서 440k steps만큼 inpainiting 학습
- UNet은 5개의 채널을 받음 (4 for the encoded masked-image and 1 for the mask itself)
- 여기에 대한 wegiht는 체크포인트 로드후에 zero-initalized함
- unet config에서 "in_channels": 9으로 바뀐다


## SD 2.0 && SD 2.1
- SD V2.0 LAION에서 개발한 새로운 텍스트 인코더 OpenCLIP 사용
    - 프롬프트에 잘 동작하지 않는 문제로 커뮤니티 비판을 받음
    - 너무 많이 필터링해서 충분하지 못한 학습

- SD V2.1
    - 필터링 조정하고 파인튜닝을 더함
    - artist's styles에 대해선 부족함


## SDXL

(1) Stable diffuson xl 
- [**stable-diffusion-xl-base-1.0**](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0)
- [**stable-diffusion-xl-refiner-1.0**](https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0)
- base와 refiner 두개가 필요

(2) [**stable-diffusion-xl-1.0-inpainting-0.1**](https://huggingface.co/diffusers/stable-diffusion-xl-1.0-inpainting-0.1) 

- stable-diffusion-xl-base-1.0로 초기화하고 1024x1024 해상도에서 40k 학습 (5% dropping of the text-conditioningto improve classifier-free cfg)
- UNet은 5개의 채널을 받음 (4 for the encoded masked-image and 1 for the mask itself)
- 여기에 대한 wegiht는 체크포인트 로드후에 zero-initalized함

(3) [**sdxl-turbo**](https://huggingface.co/stabilityai/sdxl-turbo) (sd_xl_turbo_1.0.safetensors)

- sdxl 1.0을 distill하였다
- Adversarial Diffusion Distillation (ADD) 으로 학습

(4) [**cosxl**](https://huggingface.co/stabilityai/cosxl)

- cosxl.safetensors
    - Cosine-Continuous EDM VPred schedule을 사용하기 위해 파인튜닝됨
        - produce the full color range from pitch black to pure white
        - improvements to the model's rate-of-change to images across each step.
- cosxl_edit.safetensors
    - Cosine-Continuous EDM VPred schedule을 사용하기 위해 파인튜닝됨
    - 이후 instructed image editing을 할 수 있도록 만듬


(5) SDXL-Lightning
- stable-diffusion-xl-base-1.0 를 distil하였다
- 1-step, 2-step, 4-step, and 8-step distilled models.



## SANA

### 메모리 소모 체크

```python
print(torch.cuda.memory_summary())
```

train.py 중간중간에 넣어서 확인
Sana/configs/sana_config/1024ms/Sana_1600M_img1024_AdamW.yaml
에서 data는 asset 아래 예시 데이터로 설정
```
data:
  data_dir: [asset/example_data]
  image_size: 1024
  caption_proportion:
```

gpu 하나만 돌릴거면 train.sh 스크립트를 다음처럼 변경
```
#/bin/bash
set -e

work_dir=output/debug
np=1


if [[ $1 == *.yaml ]]; then
    config=$1
    shift
else
    config="configs/sana_config/512ms/sample_dataset.yaml"
    echo "Only support .yaml files, but get $1. Set to --config_path=$config"
fi

TRITON_PRINT_AUTOTUNING=1 \
    torchrun --standalone --nproc_per_node=$np --master_port=15432 \
        train_scripts/train.py \
        --config_path=$config \
        --work_dir=$work_dir \
        --name=tmp \
        --resume_from=latest \
        --report_to=tensorboard \
        --debug=true \
        "$@"
```