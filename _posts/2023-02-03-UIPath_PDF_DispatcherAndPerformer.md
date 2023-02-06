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

1. `in_TransactionNumber <= in_Lst_PDF.Count`를 사용해 몇번 돌릴 것인지 설정한다.<br>
2. `out_TransactionItem = in_Lst_PDF(in_TransactionNumber-1)`로 리스트 개체를 하나씩 불러온다.<br>

##### STEP_3 Process

###### 1. 각 PDF파일의 공통 추출 Text를 뽑아온다.

1. `Arr_MicroPDF = in_TransactionItem.Split({vbLf}, StringSplitOptions.RemoveEmptyEntries)`로 PDF Text들을 줄바꿈 할때마다 배열 형식으로 만들어준다. <br>
2. `out_Str_Account_Number = Arr_MicroPDF(1).ToString`out_Str_Account_Number는 Account_Number라는 공통 추출 Text를 뽑는다. / 배열 두 번째에 Account_Number가 존재 <br>
3. for each로 Arr_MicroPDF를 돌려 조건에 맞는 Text만 Split으로 뽑아온다. <br>
4. `Str_Key = currentItem.ToString`으로 변수를 지정해준다. / 가독성을 위함 <br>
5. Swich Activty를 사용한다. <br>
6. Swich문의 조건은

   ```
   If( Str_Key.Contains("Invoice Number"), "Invoice Number",
    If( Str_Key.Contains("Invoice Date"), "Invoice Date",
    If( Str_Key.Contains("ATTN"), "ATTN",
    If( Str_Key.Contains("TOTAL AMOUNT"), "Total Amount",
    If( Str_Key.Contains("This invoice is for the billing period"), "Month", "Default")))))
   ```

   간략하게 설명하자면

   - Str_key 값이 Invoice Number를 포함하고 있으면 Invoice Number일 때로 이동해라 이 뜻이다. <br>
   - Str_key 값이 Invoice Date를 포함하고 있으면 Invoice Date일 때로 이동해라 이 뜻이다. <br>
   - Str_key 값이 ATTN를 포함하고 있으면 ATTN일 때로 이동해라 이 뜻이다. <br>
   - Str_key 값이 TOTAL AMOUNT를 포함하고 있으면 TOTAL AMOUNT일 때로 이동해라 이 뜻이다. <br>
   - Str_key 값이 This invoice is for the billing period를 포함하고 있으면 Month일 때로 이동해라 이 뜻이다. <br>
   - Default일 때는 그냥 통과 <br>

   a. Invoice Number 일때 작업 실행은 <br>
   `Not currentItem.ToString.Contains("Original")` <br>
   Original을 포함하지 않으면 <br>
   `out_Str_Invoice_Number = currentItem.ToString.Split(":"c)(1).ToString`
   배열로 줄이 바뀔때마다 한 줄씩 들어오므로 간단하게 split이 가능하다. <br>
   ':'로 스플릿 해서 Invoice_Number를 이런 방식으로 추출한다. <br>
   그리고 주의해야 할 점은 Original Invoice Number도 있기 때문에 if문을 사용해 조건을 걸어준다. <br>

   b. 나머지들 추출방법 <br>

   ```
   out_Str_Invoice_Date = currentItem.ToString.Split({"Date:"}, StringSplitOptions.RemoveEmptyEntries)(1).ToString.Trim <br>
   out_Str_ATTN = currentItem.ToString.Split(":"c)(1).ToString.Trim
   out_Str_Month =  currentItem.ToString.Split({"period"}, StringSplitOptions.RemoveEmptyEntries)(1).Split("1"c)(0).ToString.Trim

   ```

   C. 값이 조금씩 다른 경우 <br>
   ```currentItem.ToString.Split("$"c)(1).ToString.Trim.Contains(")")``` 
   Total Amount를 긁어 올때, ")"가 있을때, 없을때가 있기 때문에 조건을 걸어 준다. <br>


   ```
   // ")"가 있으면,
   out_Str_Total_Amount = "$"+currentItem.ToString.Split("$"c)(1).ToString.Split(")"c)(0).ToString
   // ")"가 없으면,
   out_Str_Total_Amount= "$"+currentItem.ToString.Split("$"c)(1).ToString.Trim
   
   ```

7. 각 PDF 마다 특징있는 값 가져오기 <br>
   if로 조건을 건다. 특징이 중첩 될 경우 2중 if문을 사용한다. <br>
   Credit Memo를 가져오는 것을 예시 / 편의를 위해 Python 형식으로 적겠음 <br>

우선 타겟은 Original_Invoice_Number의 값을 추출하기 위함이다. <br>

```Python
if in_TransactionItem.Contains("Credit Memo") :
	if in_TransactionItem.Contains("Premium Support") :
		out_Str_Classification = "일반 Invoice"
		io_Str_Remark = "Supporting Fee"
		out_Str_Original_Invoice_Number = ""
	else :
		out_Str_Original_Invoice_Number = in_TransactionItem.Split({"Original Invoice Number:"}, StringSplitOptions.RemoveEmptyEntries)(1).Split({"ATTN"}, StringSplitOptions.RemoveEmptyEntries)(0).ToString.Trim
		out_Str_Classification = "Credit Memo"
else :
	out_Str_Original_Invoice_Number = ""
```

정리하자면 Credit Memo를 가진 PDF는 Credit Memo_PDF와 Supporting Fee.PDF가 존재한다. 그렇기 때문에 2중 if문을 사용해줘야한다. 그리고 하는 김에 Supporting Fee.PDF의 특징 값도 가져오는 것이다.<br>

a. Credit Memo를 가지고 있는지 유무를 판단 > 없으면 Original_Invoice_Number 값은 "" 공백으로 처리 <br>
\*\*\*\* <b> 이게 중요한데 공백으로 처리하지 않으면 Queue에 null값으로 들어가기 때문에 추후에 문제가 생김 그래서 무조건 값이 없을 때에는 ""으로 공백처리를 해줘야한다. </b> <br>

b. Premium Support를 가지고 있는지 유무를 판단
Premium Support를 가지고 있으면

```
out_Str_Classification = "일반 Invoice"
io_Str_Remark = "Supporting Fee"
out_Str_Original_Invoice_Number = ""

```

Premium Support를 가지고 있지 않으면

```
out_Str_Original_Invoice_Number = in_TransactionItem.Split({"Original Invoice Number:"}, StringSplitOptions.RemoveEmptyEntries)(1).Split({"ATTN"}, StringSplitOptions.RemoveEmptyEntries)(0).ToString.Trim
out_Str_Classification = "Credit Memo"

```

<b> 나머지도 이런식으로 찾아야한다. 이것이 핵심</b> <br>

1.  변수에 null값이 존재하면 안되므로 ""을 사용하여 빈값을 꼭채워넣어야한다.<br>
2.  각 PDF에 비슷한 특징이 있으면 이중 if문을 사용해야한다.<br>

3.  Queue에 집어 넣기

필요한 값들의 변수를 Queue에 저장하면 된다. <br>

a. Queue에 집어넣는 Activity는 Add Queue Item을 사용 <br>
b. Orchestrator의 폴더 경로 설정(펼치면 선택할 수 있음) <br>
c. 큐 이름 > 큐 이름은 Orchestrator에서 Queue를 하나 생성하고 생성한 Queue의 이름을 선택해주면 됨 <br>
d. Item Information에 Dictionary처럼 Key값과 Value값을 적어서 저장해준다. (Dictionary는 아니지만 이해를 돕기위해 표현) <br>

### 2. Performer로 Queue를 가져와 Excel로 만들기

##### STEP_1 InitAllApplication

1. 최종 파일 Excel이름을 'Invoke\_통합\_yyyy-MM-dd.xlsx'로 해야한다. <br>
2. ` Today.ToString("yyyy-MM-dd")를 써서 폼을 만들어 준다. <br>
3. 저장할 파일 위치 이름을 변수로 받아 준다. <br>
   `out_Str_OutPut_Temp_Path = in_Config("OutPut_Path").ToString+"\"+in_Config("Final_Report_Name").ToString.Replace("yyyy-MM-dd", Str_Today)`
   여기에서 중요한 것은 Replace 부분이다.
4. 그리고 똑같은 날짜의 파일 이름이 존재 한다면 지워준다. (파일 초기화)
5. Template 복사 후 진행

##### STEP_2 Get Transaction Item

1. InitAllApplications는 생략한다. Queue를 사용할 때는 필요없다. 기본적인 설정이 필요할 때 사용 <br>
2. Get Queue Item Activity 사용해서 Orchestrator에서 Queue값을 가져온다. <br>
3. Config에서 OrchestratorQueueFolder와 OrchestratorQueueName을 가져온다. / 미리 Config에 설정하기 <br>
4. 그러면 QueueItem을 알아서 가져온다. <br>

##### STEP_3 Process

1. Process에서는 Add Data Row로 Template.Clone에 쌓아준다. <br>
2. 인수로 QueueItem을 받아준다 받아주는 방법은 <br>

   ```
   in_Str_Month = in_TransactionItem.SpecificContent("Month").ToString
   in_Str_Classification = in_TransactionItem.SpecificContent("Classification").ToString
   in_Str_Invoice_Date = in_TransactionItem.SpecificContent("Invoice_Date").ToString
   in_Str_Invoice_Number = in_TransactionItem.SpecificContent("Invoice_Number").ToString
   in_Str_Original_Invoice_Number = in_TransactionItem.SpecificContent("Original_Invoice_Number").ToString
   in_Str_Account_Number = in_TransactionItem.SpecificContent("Account_Number").ToString
   in_Str_Account_Name = in_TransactionItem.SpecificContent("Account_Name").ToString
   in_Str_Linked_Account_Name = in_TransactionItem.SpecificContent("Linked_Account_Name").ToString
   in_Str_Duration_Start = in_TransactionItem.SpecificContent("Duration_Start").ToString
   in_Str_Amount = in_TransactionItem.SpecificContent("Amount").ToString
   in_Str_Remark = in_TransactionItem.SpecificContent("Remark").ToString
   io_DT_Final = io_DT_Final

   ```

   <b>
   in_TransactionItem의 Type은 QueueItem 이다. QueueItem의 값을 가져오려면

   `in_TransactionItem.SpecificContent("키값").ToString`

   을 해주면 된다.

3. Config에 있는 OrchestratorQueueFolder와 OrchestratorQueueName을 가져온다. / 미리 Config에 설정하기
4. 그러면 QueueItem을 알아서 가져온다.
5. 클론 DataTable인 io_DT_Final에 위에 변수 지정한 것을 배열로 넣어 준다.
   `{in_Str_Month, in_Str_Classification, in_Str_Invoice_Date, in_Str_Invoice_Number, in_Str_Original_Invoice_Number, in_Str_Account_Number, in_Str_Account_Name, in_Str_Linked_Account_Name, in_Str_Duration_Start, in_Str_Amount, in_Str_Remark}`

##### STEP_4 CloseAllapplications

1. io_DT_Final에 쌓인 DataTable을 Excel에 작성한다.
2. 끝
