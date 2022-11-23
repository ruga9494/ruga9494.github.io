---
title: Data Preprocessing
updated: 2022-11-22 20:06
---

### 데이터 전처리 

##### 데이터 불러오기

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('/content/sample_data/@preprocessing_data_member01.csv')
df
```

<div class="divider"></div>

##### 데이터 확인하기

```python
df.head(7) ## 첫 부분 7개 가져오기 // default은 5개

df.tail(7) ## 끝 부분 7개 가져오기 // default은 5개
```

<div class="divider"></div>

##### 예제 데이터의 ‘ 유입경로 ’와 ‘ 성별 ’ 에 따른 ‘ 총판매액 ’ 의 합을 pivot table 을 이용해 구하기 

```python
pd.pivot_table(data = df , index = '유입경로', values =  '총판매액', columns = '성별' , aggfunc='sum')

## 1. 데이터 설정
## 2. index 설정
## 3. values 값 설정
## 4. columns 값 설정
## 5. 값의 총합을 설정 // default 값은 'mean' 평균
```

<div class="divider"></div>

##### 예제 데이터의 모든 연속형자료에 대한 요약 통계량 확인하기

```python
df.describe()
```

<div class="divider"></div>

##### 예제 데이터의 성별을 1과 0값으로 라벨 처리 하기 (남성 = 1 , 여성 =0)

```python
df['num_sex'] = df['성별'].replace('남자',1).replace('여자',0)
```

<div class="divider"></div>

##### 성별 이 여자인 값들만 따로 추출해 새로운 테이블로 선언
```python
df_female = df[df['num_sex']==0]
```

<div class="divider"></div>

##### 예제 데이터에서 ‘ 최종주문요일 ’ 별로 ‘ 유입경로 ’ 의 ‘총구매횟수’ 의 합을 계산하고, 판매량이 가장 높은 요일과 , 해당 요일에 가장 많이 가장 많이 유입된 경로 확인하기

```python
sum_inflow = pd.pivot_table(data=df , index= '최종주문요일', values='총구매횟수', columns='유입경로', aggfunc='sum')
sum_inflow['inflow_method'] = sum_inflow.sum(axis =1)
max_week = sum_inflow.sort_values('inflow_method', ascending=False).index[0]
max_week
```

<div class="divider"></div>

##### 예제 데이터에서 ‘ 최종주문일’ 별로 ‘ 총구매횟수’ 의 총합을 계산하고 ,가장 적게 팔린 날을 확인하기

```python
## 1. 내가 한거
pd.pivot_table(data= df, index='최종주문일', values='총구매횟수', aggfunc='sum').sort_values('총구매횟수')

## 2. 강사님이 알려준거
df['최종주문일_dt'] = df['최종주문일'].apply(lambda x : str(x).split(' ')[0])
```

<div class="divider"></div>

### 그래프 그리기 복습

##### 데이터 불러오기
```python
import seaborn as sns ## seaborn 불러오기
import matplotlib.pyplot as plt 

anscombe = sns.load_dataset('anscombe') ## 기존 데이터 불러오기
anscombe

dataset_1 = anscombe[anscombe['dataset'] == 'I'] ## 그래프 그리기 전에 데이터 전처리
dataset_2 = anscombe[anscombe['dataset'] == 'II'] ## 그래프 그리기 전에  데이터 전처리
dataset_3 = anscombe[anscombe['dataset'] == 'III'] ## 그래프 그리기 전에  데이터 전처리
dataset_4 = anscombe[anscombe['dataset'] == 'IV'] ## 그래프 그리기 전에  데이터 전처리
```

<div class="divider"></div>

##### 스케터 느낌스로 그리기

```python
plt.plot(dataset_1['x'], dataset_1['y'],'o')
```

<div class="divider"></div>

##### 그래프 연달아 그리기

```python
fig =plt.figure(figsize=(10,7)) ## 그래프 크기 늘리기

axes1 = fig.add_subplot(2,2,1) ## 2*2 1번째
axes2 = fig.add_subplot(2,2,2) ## 2*2 2번째
axes3 = fig.add_subplot(2,2,3) ## 2*2 3번째
axes4 = fig.add_subplot(2,2,4) ## 2*2 4번째

axes1.plot(dataset_1['x'],dataset_1['y'],'o')
axes2.plot(dataset_2['x'],dataset_2['y'],'o')
axes3.plot(dataset_3['x'],dataset_3['y'],'o')
axes4.plot(dataset_4['x'],dataset_4['y'],'o')

axes1.set_title('dataset_1') 
axes2.set_title('dataset_2')
axes3.set_title('dataset_3')
axes4.set_title('dataset_4')

fig.suptitle('Anscombe Data', size=20,  y=1.03)

fig.tight_layout()
```

<div class="divider"></div>

##### histplot 

```python
tips = sns.load_dataset('tips')
x = sns.histplot(tips['total_bill'])
x.set_title('Total Bill Histogram')
```

<div class="divider"></div>

##### barplot

```python
ax = sns.barplot(data = tips, x ='time', y='total_bill')
ax.set_title('Total Bill Bar Plot')
ax.set_xlabel('Time of Day')
ax.set_ylabel('Average Total Bill')
```

<div class="divider"></div>

##### boxplot

```python
sns.boxplot(data = tips, x='time', y='total_bill')
```

<div class="divider"></div>

##### violinplot

```python
sns.violinplot(data = tips, x='time', y='total_bill')
sns.violinplot(data = tips, x='time', y='total_bill', hue='sex') ## 남녀로 나눠서 구분
sns.violinplot(data = tips, x='time', y='total_bill', hue='sex', split = True) ## 남녀로 구분하는데 바이올린 그래프를 반을 짤라서 남녀로 표현
```

<div class="divider"></div>

##### barplot

```python
sns.barplot(data = tips, x='time', y='total_bill', hue = 'sex')
```

<div class="divider"></div>

##### countplot

```python
sns.countplot(data= tips, x = 'day')
```

<div class="divider"></div>

##### countplot

```python
sns.countplot(data= tips, x = 'day', order= tips['day'].value_counts().index) ## order는 tips의 day 컬럼을 개수로 정렬 시킨 후 그래프 그리기 (이쁘게 그리기)

sns.countplot(data = df, x ='최종주문요일')

```

<div class="divider"></div>

##### 연령대 만들기 

```python
def age_group(x):
  result = x // 10
  result_1 = result *10
  return result_1

df['연령대'] = df['나이'].apply(age_group)
sns.countplot(data=df, x='연령대', hue='성별')
```

<div class="divider"></div>

##### distplot

```python
sns.distplot(df['최종주문일자'])
sns.distplot(df['가입월'])
```

<div class="divider"></div>

##### lineplot

```python
sns.lineplot(data=df, x='최종주문월', y='총순수이익')
### x축 : 최종주문월 // y축 : 총순수이익
sns.boxplot(data=df, x ='성별', y='나이')
### x : 성별 // y축 : 나이
```

<div class="divider"></div>

##### 데이터 전처리 후 그래프 그리기

```python
df['광역시,도'] = df['주소'].apply(lambda x : x.split(' ')[0])
## 주소에 담겨진 광역시, 도를 apply 불러와 lambda 사용한다. lambda는 함수를 한줄로 쓰게해줌 
# ----

## "서울특별시 강남구 광평로51길 27 (수서동)" 이렇게 나온걸 ' '을 split한 다음 1첫번째 인덱스 ([0] = 서울특별시)를 가져온다 
# ----

df.groupby('광역시')['총판매액'].sum()
## 광역시로 묶은 후 총판매액의 합을 구한다.
# ----

pd.pivot_table(data= df , index = '광역시', values='총판매액', aggfunc='sum')
## 광역시를 index로 두고 values를 총판매액둔다
# ----

df['총판매액'].describe()
## 요약 

# count    4.924000e+03
# mean     6.048520e+05
# std      1.360792e+06
# min      0.000000e+00
# 25%      9.685000e+04
# 50%      2.044700e+05
# 75%      5.380450e+05
# max      2.848858e+07
# Name: 총판매액, dtype: float64
# ----

sns.distplot(df['총판매액']) # distplot 그래프 그리기
# ----

fig =plt.figure(figsize=(15,7))

sns.barplot(data=df, x= '광역시', y='총판매액') # barplot 그래프 그리기

fig.tight_layout()
```