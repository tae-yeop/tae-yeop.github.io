
시계열 데이터 

# 데이터 전처리
- 시계열 데이터에서 해줘야 하는 전처리
## 결측치 처리 (Missing Values)
- 다른 모달리티의 경우 비어있어도 통계적인 부분은 차이가 없다고 가정함(평균, 분산의 변화가 없지 않을까)
    - 따라서 그냥 결측치가 있는 column을 삭제할 수 있음 (row가 너무 많이 삭제되지 않는선에서)
    - 혹은 imputation을 수행
    - 얼마가 나올지 유추해서 채우도록 함 (mean, median, most frequent value, ML imputation, etc)


- 반면에 시계열은 비정상성 특성이라 구간별 통계량이 다름
- 또한 시계열 데이터 수집은 실시간 수집인데 여러 이슈로 인해 더 자주 발생할 수 있음
- 기본 철학은 결측치가 속해 있는 구간의 정보를 사용해서 통계량을 최대한 유지하도록

[1] LOCF(Last Observation carried forward)
- 직전 관측치가 똑같다고 본다
- 구간 내의 평균과 분산을 유지할 수 있다

[2] NOCB(Next observation carried backward)
- 직후 관측치로 값을 채운다

[3] Moving Average
- 직전 N의 time window의 평균치


🥵 [1,2,3] 주의사항
- 값이 2개 동시에 연속해서 비어 있으면 동작을 하지 않음
- stastisics가 급격하게 변하기 시작하는 지점(추세의 변곡점)에선 적합하지 않음


[4] Interpolation
- 선형, 비선형, 스플라인(Spline)
- 데이터를 보고 적합한 걸 사용


[5] Modeling
- 결측치를 맞추는 모델 자체를 만들자
- 샘플수가 작아서 일반적인 모델은 맞추기는 쉽지 않을 수 있다



다양한 방법으로 missing 데이터를 채우고 어떤게 적합한지 r2_score(`sklearn.metrics.r2_score`를 통해 계산할 수 있다.

채우는 건 .fillna()를 쓰고 fillna()의 argument로 들어갈 것은 `.interpolate(method=)` , `.rolling().mean()` , `.rolling().median()` 등을 사용할 수 있다.


## Data Leakage
- 현재 시점 $t$에선 $t-1$을 포함한 이전 정보는 사용 가능, 반면에 $t+1$의 정보는 이용 X
- 만약에 $t+1$의 정보가 어떻게든 흘러들었다면 `Data Leakage`
- 만약 $t$시점에 $t+1$에 대한 실제 true 값이 아닌 예측값이 있다면 이것도 정보이기 때문에 이는 이용 가능 (왜냐면 $t$시점에서 얻을 수 있는 정보이므로)

## Dataset Split



IID 관련 실습
https://inria.github.io/scikit-learn-mooc/python_scripts/cross_validation_time.html

## Normalization

- (1) 표준화 전체 split이 먼저 선행되어야함
- (2) Trainset의 통계량 계산
- (3) Trainset을 Normalization
- (4) Trainset의 통계량을 이용해서 val, testset도 Normalization

- 이러 순서를 지키는 이유 : 만약에 전체 데이터셋를 Normalization을 한다면 Val, testset의 정보가 train 쪽으로 흘러들어간다. 
- 그런데 이 방법은 Non-stationary한 time series일 경우 train set의 normalization statistics를 val, testset에 적용한다면 모델 성능이 급격하게 떨어진다. 
- 주기성이 있는 Time series의 경우 어디로 나눌지 고려 해야한다. 

## Augmentation
- 학습을 위




# 모델링

## 클래식 모델
