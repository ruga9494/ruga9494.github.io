---
title: Javascript 6일차
updated: 2022-10-13 09:14
---

## Do it 한 권으로 끝내는  Html + css + 자바스크립트 웹 표준의 정석 p.550

<div class="divider"></div>

### 함수 만들기

1. 함수이름 summulit 
2. 매개변수 (x,y)
3. if 문을 사용 - 값 비교
4. 같으면 곱하고 다르면 합한다.
5. 출력

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>연습문제 1</title>
</head>
<body>
	<script>
    function sumMulti(x,y) {
			if (x === y) 
				return x*y;
			else
				return x+y;
		}

		console.log(sumMulti(2,10));
		console.log(sumMulti(10,10));
  </script>
</body>
</html>
```

<div class="divider"></div>


### parseInt 함수

출처: [어제 오늘 내일:티스토리](https://hianna.tistory.com/386)

리턴 값 
string을 정수로 변환한 값을 리턴합니다.
만약, string의 첫 글자를 정수로 변경할 수 없으면 NaN(Not a Number) 값을 리턴합니다.

```javascript
parseInt("10"); // 10
// 문자열 "10"을 숫자로 변환하여 정수 10을 리턴합니다.

parseInt("-10"); // -10
// 문자열 "-10"을 숫자로 변환하여 정수 음수 -10을 리턴합니다.

parseInt("10.9"); // 10
// 문자열 타입의 실수값은 소수점을 제거한 후, 정수값만 리턴합니다.

parseInt(10); // 10
// 파라미터로 문자열이 아닌 다른 타입의 값이 전달되면, 파라미터를 문자열로 변환하여 처리합니다.

parseInt("10n"); // 10
parseInt("10nnn13"); // 10
// 문자열의 첫글자가 숫자이고, 그 이후에 숫자가 아닌 다른 문자열이 나올 경우 숫자가 아닌 문자 이후의 값은 무시하고, 그 이전의 숫자만 정수로 변환합니다.

parseInt("    10"); // 10
// 문자열의 첫글자는 반드시 숫자여야 하지만, 처음에 오는 공백 문자는 허용됩니다.

parseInt("10      "); // 10
// 문자열의 첫글자가 숫자이면, 뒤에 오는 공백은 무시됩니다.

parseInt("k10"); // NaN
// 문자열의 첫글자가 숫자가 아니면, NaN(Not a Number)를 리턴합니다.

parseInt(""); // NaN
// 문자열에 공백이 입력되면, 문자열의 첫 글자가 숫자가 아니므로, NaN(Not a Number)를 리턴합니다.

```

<div class="divider"></div>

### 현장 함수 실습 심화

1. 내가 만든 버전
```javascript
		let customer = prompt("숫자 두 개를 입력하세요.", "10,10");
		let Num = customer.split(",");
		Num[0] = parseInt(Num[0])
    Num[1] = parseInt(Num[1])
		// console.log(customer);
		console.log(Num[0]);
		console.log(Num[1]);
    function sumMulti(x,y) {
			if (x === y) 
				return x*y;
			else
				return x+y;
		}

		console.log(sumMulti(2,10));
		console.log(sumMulti(10,10));
		alert(sumMulti(Num[0],Num[1]));
```

2. 강사님 버전
```javascript
let customer = prompt("숫자 두 개를 입력하세요.", "10,10");
		let Num = customer.split(",");
    Num[0] = parseInt(Num[0])
    Num[1] = parseInt(Num[1])
		// console.log(customer);
		// console.log(Num[0]);
		// console.log(Num[1]);
    let result
  function sumMulti(x,y) {
      if (typeof(x) != 'number' || typeof(y) != 'number') { 
        //typeof(x,y)는 위에서 parseInt로 인해 문자를 사용해도 type이 number로 바뀌기때문에 의미가 없다.
        result = "입력한 값을 확인하세요.";
      
      } else {
       x = Num[0];
       y = Num[1];
			if (x === y) {
				result = x*y;
      }else{
				result = x+y;
      }
    }
    return result;
	}
    sumMulti(Num[0],Num[1]);
		alert(result);
```
 * 하지만 작동 하지 않는다.

3. 우빈 arrange
```javascript
let customer = prompt("숫자 두 개를 입력하세요.", "10,10");
		let Num = customer.split(",");
    Num[0] = parseInt(Num[0]);
    Num[1] = parseInt(Num[1]);
		// console.log(customer);
		// console.log(Num[0]);
		// console.log(Num[1]);
    let result
  function sumMulti(x,y) {
    console.log(typeof(x));
    console.log(typeof(y));
      if (isNaN(x) || isNaN(y)) {  // isNan 함수를 사용해서 true, false를 판별한다. 
      // 문자가 들어와도 type은 number 이지만(위에 parseInt함수때문에) 값은 Nan으로 나온다. 그래서 isNaN함수를 사용해 Nan인지 아닌지 판별해준다.
      result = "입력한 값을 확인하세요.";
      } else {
			if (x === y) {
				result = x*y;
      }else{
				result = x+y;
      }
    }
      return result;
	  }
    sumMulti(Num[0],Num[1]);
		alert(result);
```

<div class="divider"></div>

### js carbon

[링크](https://momentjs.com/)

> 프로퍼티(property)는 일부 객체 지향 프로그래밍 언어에서 필드(데이터 멤버)와 메소드 간 기능의 중간인 클래스 멤버의 특수한 유형이다. 프로퍼티의 읽기와 쓰기는 일반적으로 게터(getter)와 세터(setter) 메소드 호출로 변환된다.

```javascript
 var now = new Date();
    now.toLocaleString()
    now.getFullYear()

    let obj ={
      "name":"문창일",  //프로퍼티 
      "age":"29",      //키:벨류
      "기능":function() {} //메소드
    };
```

<div class="divider"></div>

### 실습 예제
1. 어레이 두개를 생성 
2. push("노","초","파","남","보")
3. 어레이갯수는 몇개
4. 과일리스트에서 딸기를 제거
5. concat 두어레이를 합치기
6. filter 무지개색깔만 필터링
7. join 사용

```javascript
    //1.
    let rainbow = ["빨","주"]
    let frults = ["사과", "수박", "귤"]
    console.log("1." + rainbow) //1.빨,주
    console.log("1." + frults) // 1.사과,수박,귤

    //2.
    rainbow.push("노","초","파","남","보");
    console.log("2." + rainbow) // 2.2.빨,주,노,초,파,남,보

    //3.
    console.log("3.rainbow의 길이 : " + rainbow.length) // 3.rainbow의 길이 : 7 
    console.log("3.frults의 길이 : " + frults.length) // 3.frults의 길이 : 3
    
    //4.
    // delete frults[2];를 하면 empty가 나옴
    frults.pop(); 
    console.log("4." + frults); // 4.사과,수박

    //5.
    let rainbowfrults = rainbow.concat(frults);
    let frultsrainbow = frults.concat(rainbow);
    console.log("5." + rainbowfrults) // 5.빨,주,노,초,파,남,보,사과,수박
    console.log("5." + frultsrainbow) //5.사과,수박,빨,주,노,초,파,남,보


    //6.
    let filterrainbow = rainbowfrults.filter(result => rainbow.includes(result)); // 변수.includes는 true, false 나오게 끔 한다. 
    console.log("6." + filterrainbow)

    //7. join함수
    let rainbowjoin = rainbow.join(",")
    let frultsjoin = frults.join(",")
    console.log(rainbowjoin)
    console.log(frultsjoin)

  console.log("6." + filterrainbow) // 6. 6.빨,주,노,초,파,남,보
```

<div class="divider"></div>

<div class="divider"></div> 

### 책 p.570 캘린더 만들기

```javascript
var now = new Date("2020-10-15");      // 오늘 날짜를 객체로 지정
        var firstDay = new Date("2020-10-15"); // 시작 날짜를 객체로 지정

        var toNow = now.getTime();             // 오늘까지 지난 시간 (밀리초)
        var toFirst = firstDay.getTime();      // 첫날까지 지난 시간 (밀리초)
        var passedTime = toNow - tofirst;       // 첫날부터 오늘까지 지난 시간 (밀리초)

        passedTime = math.round(passedTime/(1000*60*60*24)); //밀리초를 일수로 계산하고 반올림

        document.querySelector('#result').innerText = passedTime;
```

### Toast 캘린더 만들기
* [Toast UI Calendar](https://nhn.github.io/tui.calendar/latest/)<br>
* Toast 활용법](https://blog.jounsaram.net/?p=276)

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="https://uicdn.toast.com/calendar/latest/toastui-calendar.min.css" />
    <script src="https://uicdn.toast.com/calendar/latest/toastui-calendar.min.js"></script>
</head>
<body>
    <div id="calendar" style="height: 800px"></div>
    <script>
        const Calendar = tui.Calendar;
        const calendar = new Calendar('#calendar', {
  defaultView: 'week',
  template: {
    time(event) {
      const { start, end, title } = event;

      return `<span style="color: white;">${formatTime(start)}~${formatTime(end)} ${title}</span>`;
    },
    allday(event) {
      return `<span style="color: gray;">${event.title}</span>`;
    },
  },
  calendars: [
    {
      id: 'cal1',
      name: 'Personal',
      backgroundColor: '#03bd9e',
    },
    {
      id: 'cal2',
      name: 'Work',
      backgroundColor: '#00a9ff',
    },
  ],
});
    </script>

</body>
</html>
```

## 결과물


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="https://uicdn.toast.com/calendar/latest/toastui-calendar.min.css" />
    <script src="https://uicdn.toast.com/calendar/latest/toastui-calendar.min.js"></script>
</head>
<body>
    <div id="calendar" style="height: 800px"></div>
    <script>
        const Calendar = tui.Calendar;
        const calendar = new Calendar('#calendar', {
  defaultView: 'week',
  template: {
    time(event) {
      const { start, end, title } = event;
      return `<span style="color: white;">${formatTime(start)}~${formatTime(end)} ${title}</span>`;
    },
    allday(event) {
      return `<span style="color: gray;">${event.title}</span>`;
    },
  },
  calendars: [
    {
      id: 'cal1',
      name: 'Personal',
      backgroundColor: '#03bd9e',
    },
    {
      id: 'cal2',
      name: 'Work',
      backgroundColor: '#00a9ff',
    },
  ],
});
