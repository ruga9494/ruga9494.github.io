---
title: UIPath TransationItem Double Condition
updated: 2023-01-30 14:30
---

## UIpath CNSS-Check4

### 1. TransationItem 2개 설정 방법

STEP_1
DT1(원본데이터)를 읽어온다.

STEP_2

- TransactionItem을 어떤 것을 기준을 잡을지 잘 생각한다.
- DT1의 DataRow로 TransationItem 기준을 잡을 것인지 아니면 다른 것으로 TransationItem 기준을 잡을 것인지 생각한다.
- 그래서 나는 DT1의 컬럼명 arr("시도코드명","종별코드명")으로 TransationItem 기준을 잡았다.
- LinQ를 사용해 중복 Row를 제거 해서 DT2(시도코드DT),DT3(종별코드DT)를 만들어줬다.

STEP_3

- Get Transation 부분에서 이중if문(혹은 else if)를 사용한다.
- 조건은 TransationNumber <= DT2.RowCount
- 하고 TransationNumber <= DT2.RowCount + DT3.RowCount
- else는 TransationItem = Nothing

-> 그럼 처음에는 DT2 기준으로 17번 돌고 TransationNumber가 18이 되면 DT3로 돌게 된다

<b>다중 TransationItem을 만들 수 있다.</b>
