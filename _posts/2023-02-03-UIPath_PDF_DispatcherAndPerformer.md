---
title: UIPath PDF How to Queue and Dispatch,Performer
updated: 2023-02-03 17:00
---

## UIpath CNSS-Check5

### 1. Queue 사용법 - Dispatcher Queue에 담기

##### STEP_1 InitAllApplications
1. PDF 파일들을 담을 리스트 생성 > 리스트 초기화<br>
2. For Each File In Folder Activity로 파일을 불러온다. <br>
3. Read PDF Text Activity(패키지에서 받아야한다.)로 PDF 전체를 Text로 만들어준다.<br>
4. 리스트에 Append 해준다. <br>

##### STEP_2 Get TransactionData
1. in_TransactionNumber <= in_Lst_PDF.Count를 사용해 몇번 돌릴 것인지 설정한다.<br>
2. out_TransactionItem = in_Lst_PDF(in_TransactionNumber-1)로 리스트 개체를 하나씩 불러온다.<br>

##### STEP_3 Process

###### 1. 각 PDF파일의 공통 추출 Text를 뽑아온다.
1. ```Arr_MicroPDF = in_TransactionItem.Split({vbLf}, StringSplitOptions.RemoveEmptyEntries)```로 PDF Text들을 줄바꿈 일때마다 배열 형식으로 만들어준다. <br>
2. out_Str_Account_Number는 Account_Number라는 공통 추출 Text를 뽑는다.  <br>
3. Read PDF Text Activity(패키지에서 받아야한다.)로 PDF 전체를 Text로 만들어준다.<br>
4. 리스트에 Append 해준다. <br>


-> 그럼 처음에는 DT2 기준으로 17번 돌고 TransationNumber가 18이 되면 DT3로 돌게 된다

<b>******다중 TransationItem을 만들 수 있다.******</b>

### 2. Invoke VBA를 사용하여 불필요한 컬럼삭제 그리고 열넓이 Autofit으로 만들기

##### STEP_1
- Invoke VBA란 Excel 자체 내부 함수를 설정할 수 있게 해주는 Activity다. <br>
- 보통 실행폴더 안에 txt를 만들어 그 안에 VBA함수를 만들어 놓은 다음 Invoke VBA로 불러온다.<br>

```VB

Sub DeleteMultipleSheet()
Dim sheetNames() As Variant
sheetNames = Array("Sheet1")
Sheets(sheetNames).Delete

End Sub

```

위에는 다중시트 지우기 함수이다.
arr 부분에 시트 이름만 채워주면됨

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

위에는 다중시트를 포함한 원하는 Column 넓이 자동조정이다.
 - *다중시트이기 때문에 For문을 사용한다.
