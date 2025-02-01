---
title:  "파이토치 모델링 정리"
excerpt:  "텐서를 다루는 모델을 어떻게 만들까"
categories: 
- Pytorch

tags:
- Pytorch
toc_label: TOC
toc: true
toc_sticky: true
 
date: 2025-01-21
---


학습을 위해서

# 학습 관련 라이브러리


```python
# DDP를 걸때 syncBatch가 있다면 broadcast_buffers를 True로 하는건가?
# yolo에선 아님
# https://github.com/WongKinYiu/yolov7/blob/main/train.py
if cuda and rank != -1:
        model = DDP(model, device_ids=[opt.local_rank], output_device=opt.local_rank,
                    # nn.MultiheadAttention incompatibility with DDP https://github.com/pytorch/pytorch/issues/26698
                    find_unused_parameters=any(isinstance(layer, nn.MultiheadAttention) for layer in model.modules()))
```

```python
# studioGAN에선 True로
# https://github.com/POSTECH-CVLab/PyTorch-StudioGAN/blob/master/src/models/model.py
if MODEL.backbone in ["stylegan2", "stylegan3"]:
      Gen_mapping = DDP(Gen.mapping, device_ids=[device], broadcast_buffers=False)
      Gen_synthesis = DDP(Gen.synthesis, device_ids=[device], broadcast_buffers=False)
  else:
      Gen = DDP(Gen, device_ids=[device], broadcast_buffers=synchronized_bn)

```