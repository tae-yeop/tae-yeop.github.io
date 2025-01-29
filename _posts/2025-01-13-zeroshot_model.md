---
title:  "Zero-shot model"
excerpt:  ""
categories: 
- Zero-shot
- Repesentation learning

tags:
- Zero-shot
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-13
---


# Open-vocab Detection
- 기존에 학습한 클래스가 아님에도 디텍션할 수 있는 모델들
- 애니메이션 데이터에 대해 추론해보면 잘 안됨, 학습 데이터 도메인인 자연 이미지이어야 기대한대로 동작함

## YOLO-World
- Real-Time Open-Vocabulary Object Detection
![Untitled](https://github.com/user-attachments/assets/30e98167-d7bb-47a4-947b-9deb6c3219d5)
![Untitled](https://github.com/user-attachments/assets/b0e81b07-aa31-4ebd-942e-e59bdd1a0da5)
- "animation character", "animation character wearing bag" 처럼 2D 애니메이션에 대해선 잘 안됨


## OWL-ViT & OWL-ViT2
- [Scaling Open-Vocabulary Object Detection](https://arxiv.org/abs/2306.09683)
- https://github.com/google-research/scenic/tree/main/scenic/projects/owl_vit


![Untitled](https://github.com/user-attachments/assets/129cfd99-0383-43a0-a8ed-7e633f04c9ab)

![Untitled](https://github.com/user-attachments/assets/2c177af5-3c97-4b27-aac6-ddc92585de88)
- we scale up detection data with self-training
- uses an existing detector to generate pseudo-box annotations on image-text pairs

# Reference-based
- 기존에 학습하지 않았던 (Unseen) 데이터를 레퍼런스로 줬을 때 이를 찾을 수 있도록 함

## Image-Guided Zero-Shot Object Detection in Video Games
- 아이콘을 주고 이를 레퍼런스 삼아서 찾아내기
- 2개의 parallel YOLO backbone model을 사용해서 아이콘 이미지와 기존 이미지를 별도로 받을 수 있게 함

## OWL-ViT+CNN
- https://github.com/melihsrn/OWL-ViT_with_enhanced_query_embedding_network


![proposed_architecture](https://github.com/user-attachments/assets/ffbce195-df5f-480c-a0f0-bdf2e63d069f)

training an object detection model with visual queries to train
not only the object search/detect module but also the semantic
query encoding layers

- 

OWL-ViT is used as the base model to
train a one-shot image-guided object detection model on the
customized datasets.

- Extract query and image embeddings from the query and target images successively
    - To extract query embeddings
        - a vision transformer is used to obtain the feature vectors (tokens)
        - The tokens contain the information for each image patch
    - the target image :
        - same pre-trained vision transformer