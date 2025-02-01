
# 데이터

## 오픈 데이터 구하기
### 구글 드라이브 다운
- `gdown` 을 pip install하여 다운받을 수 있지만 다운 받는 용량이 제한되었던걸로 기억
- 기본 리눅스 명령어로 다운 받으려면 다음과 같이
- [출처](https://gist.github.com/tanaikech/f0f2d122e05bf5f971611258c22c110f)
```python
curl -L "https://drive.usercontent.google.com/download?id={fileId}&confirm=xxx" -o filename

wget "https://drive.usercontent.google.com/download?id=0B7qZV3T3041pTDMtN09pbklvdm8&export=download&confirm"
```


### 바이두 다운받기
- 중국 연구들을 보면 데이터셋을 하필이면 바이두에 올려 놓는 경우가 많다
- 휴대폰 정보를 넣어서 바이두에 가입했어야 했던거 같은데 그런 과정이 싫은 경우
- motrix라는 


### 데이터 생성하기
- 생성모델로 데이터를 만드는 경우
- seed를 잘 설정하도록 하자
- 파일 무결성 확인하자 : 병렬로 대량으로 만들어서 저장하면 이미지가 깨진 상태로 저장되어 나중에 이 데이터로 인해 오류가 나기도 함


# 학습 코드



### 재현성과 결정성
- seed 고정
- 보통 torch, numpy 쪽만 고정해주면 됨
- sklearn 등 과학 계산 라이브러리는 numpy를 내부적으로 쓰므로 numpy 고정필요
- `random` 패키지는 직접 쓰지 않는한 딱히 영향미치는 곳이 없음


# 분산 학습 
- 핵심은 여러개의 장비를 통한 병렬처리를 하는 것
- 이 분야만 아예 연구하시는 팀도 있음
- 자세히 파보는게 아니면 이미 구현된 라이브러리만 잘 활용해서 가치를 만드는 것에 집중하는게 나음


## Data Parallelism



## Optimizer



## 기타 메모리 줄이는 팁

### Activation Checkpoint


### Gradient Accumulation Trick
- 미니배치 한번 뽑고 forward-backward 하는게 아니라 backward를 잠시 멈추고 미니배치를 여러 번 forward 시켜서 축적한 뒤에 backward를 하자.
- 즉 원래 미니 배치 사이즈가 32이고 accmulation step에 2라면 16개씩 미니배치를 forward 넣어 축적을 시킴



