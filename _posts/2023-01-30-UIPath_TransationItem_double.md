---
title: UIPath TransationItem Double Condition
updated: 2023-01-30 14:30
---

## UIpath CNSS-Check4

### 1. TransationItem 2개 설정 방법

STEP_1
- DT1(원본데이터)를 읽어온다.

STEP_2
- TransactionItem을 어떤 것을 기준을 잡을지 잘 생각한다.<br>
- DT1의 DataRow로 TransationItem 기준을 잡을 것인지 아니면 다른 것으로 TransationItem 기준을 잡을 것인지 생각한다.<br>
- 그래서 나는 DT1의 컬럼명 arr("시도코드명","종별코드명")으로 TransationItem 기준을 잡았다.<br>
- LinQ를 사용해 중복 Row를 제거 해서 DT2(시도코드DT),DT3(종별코드DT)를 만들어줬다.<br>

STEP_3
- Get Transation 부분에서 이중if문(혹은 else if)를 사용한다.<br>
- 조건은 TransationNumber <= DT2.RowCount<br>
- 하고 TransationNumber <= DT2.RowCount + DT3.RowCount<br>
- else는 TransationItem = Nothing<br>

-> 그럼 처음에는 DT2 기준으로 17번 돌고 TransationNumber가 18이 되면 DT3로 돌게 된다

<b>다중 TransationItem을 만들 수 있다.</b>

### 2. Invoke VBA를 사용하여 불필요한 컬럼삭제 그리고 열넓이 Autofit으로 만들기

STEP_4
- Invoke VBA란 Excel 자체 내부 함수를 설정할 수 있게 해주는 Activity 이다. <br>
- 보통 실행폴더 안에 txt를 만들어 그 안에 VBA함수를 만들어 놓은 다음 Invoke로 불러온다.<br>

```VB

Sub DeleteMultipleSheet()
Dim sheetNames() As Variant
sheetNames = Array("Sheet1")
Sheets(sheetNames).Delete

End Sub

```

위에는 다중시트 지우기 함수이다.

```VB
Sub Columns_Width()

	Dim Count As Integer
	DIm i As Integer

	Count = ActiveWorkbook.Worksheets.Count

	For i = 1 To Count

		Worksheets(i).Activate
		Columns("A:E").EntireColumn.AutoFit

	Next

End sub
```

위에는 다중시트 원하는 Column 넓이 자동조정이다.
