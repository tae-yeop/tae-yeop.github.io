

# 데이터 사이언스 토픽

## IID
머신러닝에선 데이터가 i.i.d라고 가정한다.

새로운 샘플을 만들어는 generative process가 과거 샘플의 메모리가 없다고 가정하는 것이다.

보통 time series를 다룰 때 이것이 성립하지 않는다. 

샘플이 이전 정보에 depend하기 떄문



# Tree 기반
## Decision Tree
피처를 보고 대부분의 경우 실수, categorical value 등을 기준으로 나누게 된다

결과로 나온것들이 homogenous하다면 잘 분류를 한 것

피처를 어떻게 나눌지는 보통 두 가지 기준을 사용

- Gini Impurity : Shannon entropy의 특수한 경우
    - 0이면 pure하다는 것

최종 그룹이 몇 개 남을지를 파라미터로 정한다

## Random Forest

Decision Tree와 다른점

- 전체 데이터를 쓰지 않고 무작위로 뽑힌 일부를 학습에 사용
- 피처를 일부만 사용하도록 함
- 트리를 여러 개 만들어서 평균을 내서 사용한다 ⇒ Tree=weak predictor ⇒ Forest


## Gradient Tree-boosting
Boosting

- 첫번쨰 모델을 첫번째 데이터셋에 학습하고 틀리는 부분이 있음
- 그것을 보정해주는 두번쨰 모델을 만듬
- 이후 이 둘의 예측을 합쳐서 최종 결과를 낸다

eta는 1이하의 상수를 사용

### 대표 라이브러리

XGBoost, LightGBM