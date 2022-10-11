---
title: 딥러닝/인공지능 - Perceptron
updated: 2022-10-04 22:24
---

### 학습영상

url : [영상1](https://www.youtube.com/watch?v=C2sqt9pG6K0&ab_channel=%EC%BD%94%EB%94%A9%ED%95%98%EB%8A%94%EA%B1%B0%EB%8B%88) <br>
url : [영상2](https://www.youtube.com/watch?v=mRnXgBDf_oE&ab_channel=%EC%A1%B0%EC%BD%94%EB%94%A9JoCoding)

<div class="divider"></div>

### 퍼셉트론이란?
> 퍼셉트론(perceptron)은 인공신경망의 한 종류로서, 1957년에 코넬 항공 연구소(Cornell Aeronautical Lab)의 프랑크 로젠블라트 (Frank Rosenblatt)에 의해 고안되었다.

 - 다양한 정보(데이터)를 학습시킨다.
 - 순입력함수
  1. 각 데이터를 딥러닝 함
  2. 사전훈련 (딥러닝) 
 - 활성함수
  1. 임계치를 나타냄 
  2. -1 또는 1 

<div class="divider"></div>

### 다층 퍼셉트론
 > 순입력함수 부분에서 모든 경우의 수를 구한다. (몰?루)

- 다만 히든레이어(모든경우의 수를 늘려주는 부분)가 많으면 정확도가 떨어짐
 > 역전파법에서 검산할 때 오류가 발생할 확률이 높기 때문에

### 역전파법
 > 결과를 보고 다시한번 확인함 (검산)

### CNN (Covulutional Neural Network)
 - 합성곱 신경망

<div class="divider"></div>

### 머신러닝/ 딥러닝

#### 머신러닝
빅데이터 -> 학습알고리즘 -> 모델(y=wx+b) -> 새로운 데이터 삽입 -> 예측판단

#### 딥러닝
빅데이터 -> 인공 신경망 알고리즘(퍼셉트론) -> 모델(y=wx+b) -> 새로운 데이터 삽입 -> 예측판단

<div class="divider"></div>

### 전이학습(Transfer learning)
- 기존에 존재하는 빅데이터 모델안에 마지막 레이어에 새로운 데이터를 삽입 후 데이터를 학습 시킴
> Small Data -> Custom Class + 퍼셉트론 -> New Model

google 에서만든 Teachable Machine이 있음
https://teachablemachine.withgoogle.com/

### 발전하는 인공지능 사례
1. GPT-3 > Text로만 적으면 코드를 구현해줌
2. SQL 쿼리 제작 인공지능 
3. Copilot > 주석 작성하면 자동 코딩작성해줌
4. KoGPT > 카카오 한국 인공지능