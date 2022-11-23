---
title: Data Preprocessing
updated: 2022-11-23 20:18
---

## Concat과 Merge

#### Concat 연습하기

```python
from google.colab import drive
drive.mount('/content/drive')

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

!sudo apt-get install -y fonts-nanum
!sudo fc-cache -fv
!rm ~/.cache/matplotlib -rf
plt.rc('font', family='NanumBarunGothic') 

df1 = pd.read_csv("/content/drive/MyDrive/data/concat_1.csv")
df2 = pd.read_csv("/content/drive/MyDrive/data/concat_2.csv")
df3 = pd.read_csv("/content/drive/MyDrive/data/concat_3.csv")
```

<div class="divider"></div>

아래는 df1

| index | A  | B  | C  | D  |
| :--:  |:--:|:--:|:--:|:--:|
| 0     | a0 | b0 | c0 | d0 |
| 1     | a1 | b1 | c1 | d1 |
| 2     | a2 | b2 | c2 | d2 |
| 3     | a3 | b3 | c3 | d3 |

<div class="divider"></div>

아래는 df2

| index | A  | B  | C  | D  |
| :--:  |:--:|:--:|:--:|:--:|
| 0     | a4 | b4 | c4 | d4 |
| 1     | a5 | b5 | c5 | d5 |
| 2     | a6 | b6 | c6 | d6 |
| 3     | a7 | b7 | c7 | d7 |

<div class="divider"></div>

아래는 df3

| index | A  | B  | C  | D  |
| :--:  |:--:|:--:|:--:|:--:|
| 0     | a8 | b8 | c8 | d8 |
| 1     | a9 | b9 | c9 | d9 |
| 2     | a10| b10| c10| d10|
| 3     | a11| b11| c11| d11|

<div class="divider"></div>

```python
row_concat = pd.concat([df1,df2,df3], ignore_index = True)
row_concat
```

| index | A  | B  | C  | D  |
| :--:  |:--:|:--:|:--:|:--:|
| 0     | a0 | b0 | c0 | d0 |
| 1     | a1 | b1 | c1 | d1 |
| 2     | a2 | b2 | c2 | d2 |
| 3     | a3 | b3 | c3 | d3 |
| 4     | a4 | b4 | c4 | d4 |
| 5     | a5 | b5 | c5 | d5 |
| 6     | a6 | b6 | c6 | d6 |
| 7     | a7 | b7 | c7 | d7 |
| 8     | a8 | b8 | c8 | d8 |
| 9     | a9 | b9 | c9 | d9 |
| 10    | a10| b10| c10| d10|
| 11    | a11| b11| c11| d11|

<div class="divider"></div>

##### 가로로 Concat하기

```python
row_concat = pd.concat([df1,df2,df3], axis=1 )
row_concat
```

| index | A  | B  | C  | D  |
| :--:  |:--:|:--:|:--:|:--:|
| 0     | a0 | b0 | c0 | d0 |
| 1     | a1 | b1 | c1 | d1 |
| 2     | a2 | b2 | c2 | d2 |
| 3     | a3 | b3 | c3 | d3 |

- Concat의 컬럼이 다를 경우 새로운 컬럼을 추가하고 1. 해당 열에 값이 있으면 값을 추가하고 2. 해당 열에 값이 없으면 NaN으로 표시


#### Merge 

데이터 불러오기

```python
person = pd.read_csv('/content/drive/MyDrive/data/survey_person.csv')
site = pd.read_csv('/content/drive/MyDrive/data/survey_site.csv')
survey = pd.read_csv('/content/drive/MyDrive/data/survey_survey.csv')
visited = pd.read_csv('/content/drive/MyDrive/data/survey_visited.csv')
```

```python
o2o_merge =site.merge(visited_subset, left_on='name', right_on='site')
o2o_merge

## 1. site의 열 name과 visited_subset의 열 site가 공통컬럼
## 2. site 기준으로 왼쪽으로부터 DT를 합친다.
```

```python
ps = person.merge(survey, left_on='ident', right_on='person')
vs = visited.merge(survey, left_on='ident', right_on='taken')

# 1. person 기준으로 survey를 merge 시킨다. ident와 person은 공통컬럼
# 2. visited 기준으로 survey를 merge 시킨다. ident와 taken은 공통컬럼
```

```python
ps_vs = ps.merge(vs, left_on=['ident', 'taken', 'quant', 'reading'],
                   right_on=['person','ident', 'quant','reading'])
## 순서는 상관없음 left,right 매칭만 잘되면됌
# 1. ps 기준으로 vs를 merge 시킨다. 공통 컬럼은 각 위아래 매칭이다 (ident=person,taken=ident...)
```

#### 결측치 처리하기

1. isnull().sum() - NaN값이 몇개 있는지 확인하는 법
2. fillna(0) - NaN값을 0으로 채우기 > 극단적인 방법임 원하는 데이터의 신뢰성이 떨어짐
3. fillna(method ='bfill') - NaN값을 뒤에 값으로 채운다. (데이터프레임 기준 윗쪽방향) > 누적치일 경우 사용하면 좋음
4. fillna(method ='ffill') - NaN값을 앞에 값으로 채운다. (데이터프레임 기준 아래쪽방향)
5. interpolate() - NaN값을 예측해서 채워 놓는다. > y=ax+b의 함수로 예측하여 사용한다고 생각하셈 (보간법 = 두 점을 연결하는 방법)
6. dropna() - NaN값이 포함된 모든 행을 날린다.