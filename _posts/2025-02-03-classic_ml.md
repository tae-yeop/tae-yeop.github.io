

# Tree 기반
## Decision Tree


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