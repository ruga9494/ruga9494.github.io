---
title: UIPath LinQ and VLookup
updated: 2023-01-30 15:00
---

## UIpath CNSS-Check2

### 1. LinQ 사용법

##### STEP_1
- 기존 DT Activity보다 더 엄청 빠르게 할 수 있음
- .net 과 C# 기반으로 사용하는듯 함
- Assign으로 담아주기만 하면됨
- Value 값에는 LinQ를 적어주면됨

##### STEP_2
```LinQ
(
From row In DT_Templete_Cast.AsEnumerable
Select Convert.ToString(row("점코드"))
).ToList
```

```
Lst_DotCode = 
(
From row In DT_Templete_Cast.AsEnumerable
Select Convert.ToString(row("점코드"))
).ToList
```

DT1(기존데이터)에서 점코드 Column만 쭉 가져온다 (1초도 안걸림)
(참고로 list로 가져옴)

<br>

##### STEP_3
- Lst_DotCode를 기준으로 DT1(기존데이터)를 필터링 해주면 끝

<br>

### 2. VLookup 사용법

##### STEP_1

Lookup Data Table의 모양은
1. 데이터 테이블 : (어떤데이터 테이블을 기준으로 셋팅 할것인가/ 기준이되는 DT)<br>
2. 열 : (보통 빈칸?) <br>
3. 열 이름 : 어떤 Column 기준으로 찾을 것인가 <br>
4. 열 인덱스 : 기준이 되는 Column의 인덱스 (ex. 1,2,3,4...) <br>
5. 조회 값 : 찾은 값을 입력해주는 DT Column을 적어주면 된다.

적고 보니 이해가 잘안갈 것 같음 걍 googling 하는게 빠를듯 싶다.



