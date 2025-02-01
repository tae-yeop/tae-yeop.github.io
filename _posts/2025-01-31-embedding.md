
임베딩을 찾아서...


결국엔 임베딩을 얻는 것이다.
해당 데이터에 대해 압축적이고 유용한 정보를 담고 있다고 보면 됨

사전에 정의된 객체 카테고리에 한정되어 동작하는것 실제 사용에 제한을 준다
비트겐슈타인이 말한 "나의 언어의 한계가 자신의 세계의 한계다" 와 일맥상통한다
그런데 이때 매번 새로운 컨셉이 나왔을 때 마다 학습하게 해야하는걸까?


이후 이런 임베더에서 임베딩을 뽑아서 파인튜닝을 하던 제로샷(학습 과정중에 보지 못한 데이터세 대해서도 동작)으로 하던 여러
다운 스트림 태스크에 활용할 수 있다는게 핵심 논지임

일반화 능력이 제대로 보장되지 않으면 비싼 돈들여서 학습하는 이유가 없을테니



또한 이건 SSL의 기법을 사용하기 때문에 이와도 연관이 됨

Vectorization을 수행



# 데이터셋
| Dataset      | Size   | Reference / Remarks                                  |
|-------------|--------|------------------------------------------------------|
| COCO        | 328,124 | [Lin et al., 2014]                                  |
| VG          | 108,077 | [Krishna et al., 2017]                              |
| CC          | 3.1M    | [Sharma et al., 2018]                               |
| SBU         | 1M      | [Ordonez et al., 2011]                              |
| LAION-400M  | 400M    | [LAION Project](https://laion.ai/projects/)        |
| LAION-5B    | 5.85B   | [LAION Project](https://laion.ai/projects/)        |
| RedCaps     | 12M     | [Desai et al., 2021]                                |
| COYO        | 700M    | [COYO Dataset](https://github.com/kakaobrain/coyo-dataset) |
|  WIT(WebImageText)| 4B | OpenAI CLIP Dataset (인터넷 크롤링) |


## 성능 평가 방법


# 다양한 도메인



# 대규모 임베딩

- 대규모 데이터셋의 임베딩

# 더 디테일하게
- global한 semantic을 넘어서 더 fine한 디테일까지도 임베딩에 반영하고자 함

https://www.youtube.com/watch?v=oFYsGoiMidk


# Multi modality
- 동일한 데이터에 대한 다른 표현을 지는 모달리티를 동시에 학습시킨다면?
- 예를 들어 Vision-Language를 활용한 VLM을 위해선 임베딩이 필수적

이후 이를 개선한 연구들이 쭉 나오게 된다


- 특히 라벨링만으로는 충분하지 않음
- 특히나 자연어는 같은 대상도 다양하게 표현하는 flelxible한 특성이 있음

## CLIP
![Image](https://github.com/user-attachments/assets/b0591f6b-4e9a-47af-bd45-99a2411ea8ff)
- 웹크롤링해서 얻은 자연어 텍스트와 이미지를 사용 (4억개의 이미지-텍스트)
- 이미지랑 대응되는 텍스트와 짝을 맞추도록 하자
- 짝을 맞추게끔 하다보면 결국 이미지내의 시각적인 컨셉을 잘 이해할 수 있어야 할 것이다.
- 이미지 인코더, 텍스트 인코더 모두 Transformer





- [CLIP Interrogator](https://github.com/pharmapsychotic/clip-interrogator)라는 것도 있는데 이는 역으로 이미지를 가장 잘 표현하는 text를 optimization으로 찾아낸다.
- CLIP Interrogator는 다음에 설명하는 BLIP에 기초함

## BLIP, BLIPv2
- 

[GLIP, 2021,12]()
![Image](https://github.com/user-attachments/assets/e7371ebf-e4df-4b5e-bd3d-054339837ec6)

- CLIP은 객체 단위의 세세한 디테일을 놓치는 경우가 있음
- 객체단위로 언어를 인지하면서 풍부하게 학습시키자
- self-training 방식으로 grounding gox를 만들면서 다량의 image-text 짝을 이용
- phase grounding : 문장에 있는 phrase(동사이외 두 낱말로 이루어진 구)와 객체 사이의 일치성을 확인하는 작업

[X-CLIP, 2022,07](https://arxiv.org/abs/2207.07285)
[FLIP]
[ImageBind, 2023,05](https://arxiv.org/abs/2305.05665)
[Alpha-CLIP, 2023,12](https://arxiv.org/abs/2312.03818)


# 임베딩 활용 방안
