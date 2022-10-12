---
title: Javascript 5일차
updated: 2022-10-12 09:14
---

## Do it 한 권으로 끝내는 <br> Html + css + 자바스크립트 웹 표준의 정석

<div class="divider"></div>

### 함수 

```javascript
function addNumber(a, b) {
      var sum = a + b;
      alert(sum);
    }
    console.log(addNumber(1,5));
```

* 지역변수(local variable) : 함수 같은 곳에서 할당된 변수는 그 함수내에서만 유효함
* 전역변수(global variable) : 함수 같은 곳이 아닌 넓은 곳에서 할당된 변수

```javascript
function addNumber(num1, num2) { 								
			return num1 + num2;						
		}
		var sum = addNumber(10, 20);
    console.log(sum); // sum : 30
    sum = 50;
    console.log(sum); // sum : 50
    var sum = 100;
    console.log(sum); // sum : 100
```

<div class="divider"></div>

### let 과 const 

* let - 변수선언
* const - 상수선언

```javascript
function calcSum(n) {
    let sum = 0;
    for (let i = 1; i < n + 1; i++) {
      sum += i;
    }
    console.log(sum);
   }
   calcSum(10);
```

>let - 재할당은 가능, 재선언은 불가능하다

* 들어있는 값을 바꾸는건 가능

* 같은이름으로 변수를 선언하는건 불가

> const 상수, 재선언도 불가능 (고정값인듯)

<div class="divider"></div>

### 호이스팅이 없는 변수

```javascript
var x = 10;

function displayNumber() {
	console.log("x is " + x);
	let y = 20;
	console.log("y is " + y);
}
displayNumber();
```
> 호이스팅은 선언되기전에 쓸 수 있다. 선언된 부분의 순서를 먼저사용 (위에서 순서대로 실행되기전에 이미 값이 할당 되어있음) <em>예) 함수를 아래 만들어 놓고 위에서 쓸수 있는 것처럼</em>

* var - 재선언 가능 / 재할당 가능 / 호이스팅 가능
* let - 재선언 불가능 / 재할당 가능 / 호이스팅 불가능
* const - 재선언 불가능 / 재할당 불가능 / 호이스팅 불가능

| 변수선언      | 재선언    | 재할당  | 호이스팅 |
| -----------  |:--------:| :------:| :------:|
| var          | O        |  O     | O      |
| let          | X        |  O     | X      |
| const        | X        |  X     | X      |

<div class="divider"></div>

### 이벤트와 이벤트 처리기

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>자바스크립트 이벤트</title>
	<link rel="stylesheet" href="css/function.css">
</head>
<body>
	<ul>
		<li><a href="#" onmouseover="a()">Green</a></li> // 마우스 올리면 함수작용
		<li><a href="#" onclick="alert('버튼을 클릭했습니다.')">Orange</a></li> // 누르면 알람뜸
		<li><a href="#" onclick="alert('버튼을 클릭했습니다.')">Purple</a></li>
	</ul>		
	<div id="result"></div>
  <script>
    function a() {
      alert('버트을 클릭했습니다.');
    }


  </script>
</body>
</html>  
```

버튼을 누르면 색이 바뀜
```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>자바스크립트 이벤트</title>
	<link rel="stylesheet" href="/css/function.css"> // css 주소 시작할때 / 꼭체크하기 안하면 작동안함
</head>
<body>
	<ul>
		<li><a href="#" onclick="changeBg('green')">Green</a></li>
		<li><a href="#" onclick="changeBg('orange')">Orange</a></li>
		<li><a href="#" onclick="changeBg('purple')">Purple</a></li>
	</ul>		
	<div id="result"></div>
	
	<script>
		function changeBg(color) {
			var result = document.querySelector('#result');
			result.style.backgroundColor = color;
		}
	</script>
</body>
</html>  
```

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>자바스크립트 이벤트</title>
	<link rel="stylesheet" href="/css/event.css">
</head>
<body>
	<div id="item">
		<img src="/public/images/flower.jpg" alt="">
		<button class="over" id="open">상세 설명 보기</button>
		<div id="desc" class="detail">
			<h4>등심붓꽃</h4>
			<p>북아메리카 원산으로 각지에서 관상초로 흔히 심고 있는 귀화식물이다. 길가나 잔디밭에서 흔히 볼 수 있다. 아주 작은 씨앗을 무수히 많이 가지고 있는데 바람을 이용해 씨앗들을 날려보내거나, 뿌리줄기를 통해 동일한 개체들을 많이 만들어 냄으로써 번식한다. </p>
			<button id="close">상세 설명 닫기</button>
		</div>
	</div>	

	<script>		
		document.querySelector('#open').onclick = function() {
			document.querySelector('#desc').style.display = "block";	// 상세 설명 부분을 화면에 표시
			document.querySelector('#open').style.display = "none";   // '상세 설명 보기' 단추를 화면에서 감춤
		}
		document.querySelector('#close').onclick = function() {
			document.querySelector('#desc').style.display = "none";	   // 상세 설명 부분을 화면에서 감춤
			document.querySelector('#open').style.display = "block";	 // '상세 설명 보기' 단추를 화면에 표시
		}				
	</script>
</body>
</html>  
```

응용해서 현재 날짜,시간 만들기

```javascript
<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>첫화면</title>
  <!-- 외부스크립트 -->
  <!-- <script src="path/to/script.js"></script> -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.11/lodash.js"></script>
</head>
<body>
  <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Bootstrap demo</title>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-Zenh87qX5JnK2Jl0vWa8Ck2rdkQ2Bzep5IDxbcnCeuOxjzrPF/et3URy9Bv1WTRi"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <p id="time"></p>
    <button id="open">시간보기</button>	
    <button id="close">시간닫기</button>

    <script>
      let today = new Date();
      console.log(today);	
      
      document.getElementById('open').onclick = function() {
        document.getElementById('time').innerHTML = today;	   // 상세 설명 부분을 화면에서 감춤
      }			
      document.getElementById('close').onclick = function() {
        document.getElementById('time').innerHTML = "";	   // 상세 설명 부분을 화면에서 감춤
      }		
    </script>
  </body>
</html>
</body>
</html>
```