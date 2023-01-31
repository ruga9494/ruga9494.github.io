---
title: UIPath LinQ and Invoke Method
updated: 2023-01-30 15:30
---

## UIpath CNSS-Check_1-1

### 1. LinQ 사용법

##### STEP_1
- 기존 DT Activity보다 더 엄청 빠르게 할 수 있음
- .net 과 C# 기반으로 사용하는듯 함
- Assign으로 담아주기만 하면됨
- Value 값에는 LinQ를 적어주면됨

##### STEP_2

```LinQ
DT1.AsEnumerable().GroupBy(Function(i) i.Field(Of String)("이름")).Select(Function(g) g.Last).CopytoDataTable()
```

중복 행을 지우면서 마지막에 있는 행을 남긴다 라는 뜻
Last를 First로 바꾸면 첫번째 행을 가져온다는 뜻<br>



### 2. Invoke Method 사용법

##### STEP_1

Invoke Method 사용법
 - 보통 Column의 순서를 바꿔줄 때, 사용하는 것 같음

1. TargetObject에 순서를 바꾸려는 Column을 적는다. 

```
DT3.Columns("번호")
```

2. MethodName에는 'SetOrdinal'이라는 것을 적는다.
3. 'SetOrdinal' 이게 첫번째 열로 바꿔는건가? 그건 잘 모르겠다.
4. 결국 중효한 것은 구글링

적고 보니 이해가 잘안갈 것 같음 걍 googling 하는게 빠를듯 싶다.



