---
title: UIPath LinQ and VLookup
updated: 2023-01-30 15:00
---

## UIpath CNSS-Check2

### 1. LinQ 사용법

STEP_1
- 기존 DT Activity보다 더 엄청 빠르게 할 수 있음
- .net 과 C# 기반으로 사용하는듯 함
- Assign으로 담아주기만 하면됨
- Value 값에는 LinQ를 적어주면됨

STEP_2

```LinQ
(
From row In DT_Templete_Cast.AsEnumerable
Select Convert.ToString(row("점코드"))
).ToList

```


STEP_3



-> 그럼 처음에는 DT2 기준으로 17번 돌고 TransationNumber가 18이 되면 DT3로 돌게 된다

<b>다중 TransationItem을 만들 수 있다.</b>
