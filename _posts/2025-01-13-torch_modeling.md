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
 
date: 2025-01-13
---


파이토치 관련 정리

# 기본 텐서 연산 (tensor ops)
- 대부분 `torch.Tensor` 의 메소드로 들고 있으면 `torch` 모듈에도 같은 함수가 있음
- 예외적으로 `.expand()`는 `torch.Tensor`에만 있었음

## 텐서 연산 특징
- 연산결과로 나오는 리턴이 인풋과 같은 저장 공간(storage)를 공유하는 경우가 있다
```python
t = torch.randn((2,5))
>>>
tensor([[ 0.0885,  0.6537, -1.3698, -0.3036, -0.2779],
        [ 0.3918, -0.4049,  1.6175,  0.9610,  0.5304]])

tuples_of_tensors = torch.split(t, 2,dim=1)
tuples_of_tensors[0].shape
>>>
torch.Size([2, 2])

len(tuples_of_tensors)
>>>
3

tuples_of_tensors[0]
>>>
tensor([[ 0.0885,  0.6537],
        [ 0.3918, -0.4049]])

tuples_of_tensors[1]
>>>
tensor([[-1.3698, -0.3036],
        [ 1.6175,  0.9610]])

tuples_of_tensors[2]
>>>
tensor([[-0.2779],
        [ 0.5304]])


t.storage() == tuples_of_tensors[2].storage()
>>>
0.0884939506649971
 0.6537140011787415
 -1.3697537183761597
 -0.30357104539871216
 -0.27787643671035767
 0.3917590379714966
 -0.40486636757850647
 1.6175081729888916
 0.9610353112220764
 0.5303764343261719
[torch.FloatStorage of size 10]
```

## Broadcasting

## 합치거나 나누거나
- 자주 쓰이는 `torch.cat()` 외에 몇 가지


- `torch.stack()` : cat과 다른 점은 새로운 차원을 만듬, 예를 들어 이미지 3개를 합쳐 배치축에 올리려면 다음과 같이 함

```python
import torch

# 세 개의 3채널 이미지 텐서 (C, H, W)
img1 = torch.randn(3, 224, 224)
img2 = torch.randn(3, 224, 224)
img3 = torch.randn(3, 224, 224)

# 배치 차원으로 쌓기 (B, C, H, W)
batch = torch.stack([img1, img2, img3])
print(batch.shape)  # 출력: torch.Size([3, 3, 224, 224])
```

- `torch.chunk()` and `torch.split()`
    - dim 방향으로 텐서를 자르고 shape를 보존해서 튜플에 담아서 리턴
    - 둘의 차이는 split은 길이를 명시해야는거고 chunk는 덩어리 갯수를 명시함
    - 정확히 나눠 떨어지지 않아도 나머지를 알아서 리턴해줌
    - 대표적인 유즈 케이스는 어탠션 매커니즘에서 head 차원으로 분리할 때 사용
    - 인풋 텐서와 리턴 텐서가 같은 storage를 공유함
```python
# 멀티 헤드 쿼리 (32배치, 8 헤드, 64차원)
query = torch.randn(32, 8 * 64)
head_chunks = torch.chunk(query, 8, dim=-1)  # 8개의 헤드로 분리
```



```python
high[0]
# [1, 3, 3, 128, 128]
torch.chunk(high[0], chunks=3, dim=2)
# (tensor[1, 3, 1, 128, 128] n=49152 x∈[-3.963, 4.404] μ=0.006 σ=1.001,
# tensor[1, 3, 1, 128, 128] n=49152 x∈[-4.418, 4.188] μ=-0.005 σ=1.000,
# tensor[1, 3, 1, 128, 128] n=49152 x∈[-4.431, 4.013] μ=-0.002 σ=0.996)
```

- `torch.split()` : 

```python
# [1, 3, 3, 128, 128] => [1, 3, 3, 128, 128]
torch.split(high[0], 3, dim=2)
# [1, 3, 3, 128, 128] => 
torch.split(high[0], 1, dim=2)
# (tensor[1, 3, 1, 128, 128] n=49152 x∈[-3.963, 4.404] μ=0.006 σ=1.001,
# tensor[1, 3, 1, 128, 128] n=49152 x∈[-4.418, 4.188] μ=-0.005 σ=1.000,
# tensor[1, 3, 1, 128, 128] n=49152 x∈[-4.431, 4.013] μ=-0.002 σ=0.996)

```

- `torch.unbind()`
    - 비슷한 녀석으로 unbind가 있는데 지정한 dim을 없애서 갈갈이 리턴함

```python
# Split the inputs into smaller chunks
sub_batches = torch.unbind(inputs.chunk(grad_accum_steps, dim=0), dim=0)  # 4 tensors of shape (4, 10)
target_batches = torch.unbind(targets.chunk(grad_accum_steps, dim=0), dim=0)  # 4 tensors of shape (4,)

# Grad accumulation loop
optimizer.zero_grad()  # Reset gradients
for sub_input, sub_target in zip(sub_batches, target_batches):
    outputs = model(sub_input)  # Forward pass
    loss = loss_fn(outputs, sub_target)  # Compute loss
    loss.backward()  # Backward pass
    # Gradients are accumulated in model parameters

```

## 중복하기

- `torch.expand()`
        - 기본적으로 outer-most(앞쪽)방향으로 dimension을 추가
        - inner-most로 추가하기 위해선 singleton dimension(dimension이 1인 것)이 반드시 필요함
        - 따라서 unsqueeze()를 먼저 쓴 뒤에 수행

```python
t1 = torch.randn(4)
>>>
tensor([-0.5156,  1.3306, -0.2606, -0.5196])
t1.unsqueeze(1).shape
>>>
torch.Size([4, 1])
t1.unsqueeze(1).expand(4, 10)
>>>
tensor([[-0.5156, -0.5156, -0.5156, -0.5156, -0.5156, -0.5156, -0.5156, -0.5156,
         -0.5156, -0.5156],
        [ 1.3306,  1.3306,  1.3306,  1.3306,  1.3306,  1.3306,  1.3306,  1.3306,
          1.3306,  1.3306],
        [-0.2606, -0.2606, -0.2606, -0.2606, -0.2606, -0.2606, -0.2606, -0.2606,
         -0.2606, -0.2606],
        [-0.5196, -0.5196, -0.5196, -0.5196, -0.5196, -0.5196, -0.5196, -0.5196,
         -0.5196, -0.5196]])

```

- `torch.repeat()`
- 

| 특징                   | `torch.expand()`                               | `torch.repeat()`                                   | `torch.repeat_interleave()`                     |
|------------------------|-----------------------------------------------|--------------------------------------------------|------------------------------------------------|
| **목적**              | 크기 확장 (메모리 복제 없이 broadcasting)     | 텐서를 지정된 크기로 복제 (메모리 복제 O)         | 요소를 지정된 횟수만큼 복제하여 1D로 확장       |
| **출력 크기**          | 입력 크기와 같은 차원을 유지하며 broadcasting | 지정된 크기에 따라 차원이 늘어남                  | 1D 텐서로 변환                                  |
| **메모리 공유 여부**   | **공유 O** (데이터 복제 없음)                 | **공유 X** (데이터 복제)                          | **공유 X** (데이터 복제)                        |
| **역전파 지원**        | 지원 O                                         | 지원 O                                           | 지원 O                                         |
| **속도 및 효율성**     | 매우 효율적 (데이터 복제 없음)                | 상대적으로 비효율적 (데이터 복제 필요)            | 상대적으로 비효율적 (데이터 복제 필요)          |
| **주요 제약 사항**     | Singleton 차원(크기 1)만 확장 가능            | 데이터 복제가 많아 메모리 사용량 증가 가능        | 차원을 늘릴 수 없음, 1D로 변환만 가능           |
| **대표 유즈케이스**    | Broadcasting 연산, 크기 맞춤                  | 텐서를 복제하여 여러 위치에서 사용                | 클래스 레이블 확장, 시퀀스 데이터 준비          |




## 선택하기
- 텐서에서 특정 부분을 취사선택할 수 있는 로직이 필요한 경우가 많다.


- 인덱스 연산자 `[]`
- `torch.index_select()`나 `torch.select()` 같은 기능을 하지만 좀 더 명시적이라 가독성이 좋음
- tensor.select(0, index) == tensor[index],  tensor.select(2, index) == tensor[:,:,index]

```python
t = torch.ones((32, 4))
t[None, 0:1].shape # torch.Size([1, 1, 4])
```
- 실제 값이 뽑히는건 다음을 보면 알 수 있다
```python
import numpy as np
d = np.array([[[i + 2 * j + 8 * k for i in range(3)] for j in range(3)] for k in range(3)])
d

array([[[ 0,  1,  2],
        [ 2,  3,  4],
        [ 4,  5,  6]],

       [[ 8,  9, 10],
        [10, 11, 12],
        [12, 13, 14]],

       [[16, 17, 18],
        [18, 19, 20],
        [20, 21, 22]]])

d[:,:,1]
>>>
array([[ 1,  3,  5],
       [ 9, 11, 13],
       [17, 19, 21]])

import torch
d_torch = torch.from_numpy(d)

d_torch[:,:,0]
>>>
tensor([[ 0,  2,  4],
        [ 8, 10, 12],
        [16, 18, 20]])

```


- `torch.gather(input, dim, index, *, out=None) → Tensor`
- 인덱싱 혹은 룩업 용도

```python
# actual use case
# Q-table에서 q(s,a)를 선택.
Q_expected = self.qnetwork_local(states).gather(1, actions)
# dim=1을 따라서 actions에 나온 index에 맞춰서 Q값을 선택

```

```python
# 정책 네트워크의 출력 (각 행동의 확률)
policy_output = torch.tensor([[0.2, 0.5, 0.3], [0.1, 0.6, 0.3]])

# 에이전트의 선택된 행동 인덱스
actions = torch.tensor([[1], [2]])

# 선택된 행동의 확률만 추출
selected_probs = torch.gather(policy_output, dim=1, index=actions)
print(selected_probs)
# tensor([[0.5],
#         [0.3]])

```

```python
# 예시: 문장의 단어 인덱스
word_indices = torch.tensor([[1, 3, 2], [0, 2, 1]])

# 단어 임베딩 행렬 (보통 임베딩 차원은 더 큼)
embedding_matrix = torch.tensor([
    [0.1, 0.2, 0.3],  # Word 0
    [0.4, 0.5, 0.6],  # Word 1
    [0.7, 0.8, 0.9],  # Word 2
    [1.0, 1.1, 1.2]   # Word 3
])

# Gather word embeddings
embeddings = torch.gather(embedding_matrix, 0, word_indices)
print(embeddings)
# tensor([[[0.4000, 0.5000, 0.6000],
#          [1.0000, 1.1000, 1.2000],
#          [0.7000, 0.8000, 0.9000]],

#         [[0.1000, 0.2000, 0.3000],
#          [0.7000, 0.8000, 0.9000],
#          [0.4000, 0.5000, 0.6000]]])
```

- `torch.scatter()` : 원핫 인코딩 만들 때 쓸 수 있음
- tensor.scatter_(dim, index, src)
- 2차원이고 `dim=0`이면 `y[index[i, j], j] = x[i, j]` 와 같음.
- 3차원이면 `dim=1`이면 `y[i][index[i,j,k][k]] = x[i][j][k]`와 같음.
- `torch.scatter_add()`는 `self[index[i][j][k]] [j][k] += src[i][j][k] # if dim == 0`와 같음

```python
import torch

# 클래스 수와 배치 크기 정의
num_classes = 5
batch_size = 3

# 레이블 텐서 (배치 크기)
labels = torch.tensor([0, 2, 4])

# 원-핫 인코딩을 위한 텐서 초기화
one_hot = torch.zeros(batch_size, num_classes)

# 레이블을 원-핫 벡터로 변환
one_hot.scatter_(1, labels.unsqueeze(1), 1)

print(one_hot)

```


- `torch.masked_select()`
- 선택사항을 불리언 마스크로 넣너줌
- 항상 1차원 텐서로 리턴
- 픽셀에서 특정 조건을 만족하는 값을 얻거나 NLP에서 zero-padding이 아닌 유의미한 값만 얻을 때 사용
```python
# 그레이스케일 이미지
image = torch.randn(1, 256, 256)

# 특정 임계값 이상인 픽셀만 추출
mask = image > 0.5
bright_pixels = torch.masked_select(image, mask)


sequences = torch.tensor([[1, 2, 0, 0],
                          [3, 4, 5, 0]])
mask = sequences > 0

# 패딩 제거 후의 토큰
tokens = torch.masked_select(sequences, mask)
print(tokens)  # tensor([1, 2, 3, 4, 5])
```





- `torch.narrow(input, dim, start, length)`
- 차원과 시작위치와 길이를 명시할 수 있음
- 잘 안씀




## Shape 바꾸기
- `reshape`, `view`, `permute`, `transpose` 를 쓰면 됨
- `permute`와 `transpose`는 Non-contiguous 텐서가 리턴되는데 대부분 파이토치 연산에선 Non-contiguous도 처리할 수 있다 (stride 정보를 이용해서)
- 하지만 Contiguous 텐서만 받는 연산이 있는데 이를 위해서라도 contiguos() 처리를 하도록한다
- 다음은 Contiguous 텐서만 받는 연산 (즉 피지컬 메모리 상에서 연속적이어야만함)
        - `torch.view()`
        - `torch.flatten()`
        - `torch.as_strided()`
        - `torch.nn.functional.fold()`
        - `torch.nn.functional.unfold()`

- 데이터 공유 관점에선 나머지는 다 공유하고 `reshape`는 Contiguos 텐서가 인풋으로 올때만 메모리를 공유함
- 메모리를 공유하게 되면 In-place연산으로 한쪽을 바꾸면 다른쪽도 바뀐다는 뜻
- 또 In-place 연산을 하면 Autograd 동작이 제대로 안됨
- flatten의 경우 아예 레이어로도 존재함 : `nn.Flatten()`
        - [내부적으로 보면 flatten()을 사용함](https://pytorch.org/docs/stable/_modules/torch/nn/modules/flatten.html#Flatten)

# 모델 만들기

## Normalization
### BatchNorm
- 최신 모델에는 잘 보이진 않지만 이전 모델이나 Head 쪽에 추가하는 경우 아직 간간히 보임
- 원리는 forward 마다 mini batch statistics를 업데이트하는 것
![Image](https://github.com/user-attachments/assets/9a229b4b-6bc2-4d4b-a01a-c2e08e4fecdf)

![Image](https://github.com/user-attachments/assets/f934dd56-34cf-4b12-9d02-cc38a01a365b)

Forward
$$
y_i = \gamma\cdot\frac{x_i-\mu}{\sigma} + \beta \\~\\
\mu=\frac{\sum_i^N x_i}{N} , \sigma = \sqrt{\frac{\sum_i^N (x_i-\mu)^2}{N}+\epsilon}
$$

Backward
$$
\frac{d_\ell}{d_{x_i}} = \frac{d_\ell}{d_{y_i}}\cdot\frac{\partial_{y_i}}{\partial_{x_i}} + \frac{d_\ell}{d_\mu}\cdot\frac{d_\mu}{d_{x_i}} + \frac{d_\ell}{d_\sigma}\cdot\frac{d_\sigma}{d_{x_i}} \\~\\

\frac{\partial_{y_i}}{\partial_{x_i}}=\frac{\gamma}{\sigma}, \frac{d_\ell}{d_\mu}=-\frac{\gamma}{\sigma}\sum_i^N\frac{d_\ell}{d_{y_i}}
\text{ and } \frac{d_\sigma}{d_{x_i}}=-\frac{1}{\sigma}(\frac{x_i-\mu}{N})
$$


- [SyncBN](https://hangzhang.org/PyTorch-Encoding/tutorials/syncbn.html)
        - DDP 상황에선 디바이스마다 다른 미니배치가 forward로 감
        - 이 때문에 mini batch statistics가 차이가 남 -> 맞출 필요성 -> 대신 속도 저하
        - 일반적인 clasification, detection의 경우 working batch size(= BatchSize/nGPU)가 크기 때문에 syncBN을 할 필요가 없다
        - 써야 하는 상황 : working batch size 작음 (GPU 당 2~4개) ⇒ Sync 필요
        - 클래스로 쓰거나 아니면 바꿔주는 유틸리티 함수를 쓰도록 함
        - torch.nn.SyncBatchNorm는 train mode일 때에만 sync가 일어남 ⇒ eval mode라면 sync가 꺼짐
        - 파이토치 라이트닝에는 sync_batch로 바꾸는 옵션이 있는데 [Fabric](https://github.com/Lightning-AI/pytorch-lightning/issues/13749)에는 없는 것처럼 보임

```python
trainer = pl.Trainer(
    max_epochs=10,
    devices="auto",
    accelerator="gpu",
    strategy="ddp",
    sync_batchnorm=True,
    use_distributed_sampler=True,
)
```