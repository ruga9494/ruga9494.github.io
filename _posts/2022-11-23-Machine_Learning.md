---
title: Machine Leaning 
updated: 2022-11-23 21:00
---

### Machine Leaning 

```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
import pandas as pd
from sklearn.datasets import load_breast_cancer
import pandas as pd
cancer_data = load_breast_cancer()

# 데이터를 가져와 x,y에 담는다
X = pd.DataFrame(cancer_data.data, columns=cancer_data.feature_names) # input data
y = pd.DataFrame(cancer_data.target, columns=['class']) # target data

# 훈련데이터와 테스트데이터를 나눈다 // y는 결과값
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.2) 
# test_size는 데이터의 20%를 테스트용으로 쓰겠다는 말 20~30%가 적당

# 의사결정 나무 모델을 생성한다. // 깊이는 3이라는 뜻 // depth가 너무 깊으면 오버피팅남
model = DecisionTreeClassifier(max_depth = 3)

# 훈련데이터를 의사결정 나무에 넣는다
model.fit(x_train,y_train)

# predict(예측하다) // x_test값을 예측한다.
model.predict(x_test)

# 만든 모델의 정확도 계산 // 1에 가까울수록 좋음
model.score(x_test, y_test) # 0.9122807017543859
```

### 스케일 변환

* 1000점의 100점과 100점의 90점이 있다 가정하자 // <br> 1000점의 100점은 총점에 비해 너무 작은 점수를 가지고 있다. 그렇기 때문에 크기를 좀 줄여서 정확도를 높이는 것이 스케일 변환이다.

1. StandardScaler(표준화) : 평균을 0, 분산을 1로 변경하여 같은 크기를 가지게 한다.
2. RobustScaler : 중간값과 사분위 값을 사용하며 StandardScaler과 유사하다 <br>
   • 이상치(outlier)의 영향을 덜 받는다.

3. MinMaxScaler(정규화) : 모든 데이터가 0~1사이에 위치하도록 데이터를 변경
4. Normalizer : 벡터의 유클리디안 길이가 1이 되도록 조정 <br>
• 지름이 1인 원 or 구에 데이터를 투영 <br>
• 벡터의 길이가 중요하지 않고 벡터의 방향(각도)가 중요할 때 많이 사용

```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
import pandas as pd
from sklearn.datasets import load_breast_cancer
cancer_data = load_breast_cancer()

# 암데이터를 불러온다.
X = pd.DataFrame(cancer_data.data, columns=cancer_data.feature_names) # input data
y = pd.DataFrame(cancer_data.target, columns=['class']) # target data

#train_test_split 함수를 활용하여 데이터를 분리
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# MinMaxScaler을 불러와 훈련데이터안에 집어넣어 적당한 사이즈로 만들어준다.
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
scaler.fit(x_train)

# 여기서부터 모름 학원가서 물어봐야함
```