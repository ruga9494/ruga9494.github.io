---
title: Javascript 7일차
updated: 2022-10-17 09:05
---



<div class="divider"></div>

## javascipt 변수, 자료형, 출력문, 연산자, 제어문

공부출처[링크1](https://www.youtube.com/watch?v=1EUHLzBsE20&list=PLkRxB9FjUuPwUyG0VrP6mZJ25S3rUX_pG&index=15&t=906s&ab_channel=%ED%99%A9%ED%9D%AC%EC%A0%95%EC%A7%A7%EA%B5%B5%EB%B0%B0)

### 1. 자료형

내부적으로는 Primitive(기본형)과 Object(객체형)이 있다.

##### Primitive
* Boolean : true, false
* null: 빈 값을 표현
* undefined : 값을 할당하지 않은 변수가 가지는 값
* Number: 숫자형으로 정수와 부동 소수점, 무한대 및 NAN(숫자가 아님을 뜻하는 숫자형) 등.
* String : 문자형

##### Object
* Reference 타입
* 클래스 뿐만 아니라, 배열과 함수, 사용자 정의 클래스 모두 Object이다
* JSON(Java Script Object Notation)의 기본 구조.

Object에 대해서는 06. 함수와 객체에서 자세히 다룸

<div class="divider"></div>

### 2. 변수 선언
* 변수이름은 대소문자를 구별
* 여러 변수를 한번에 선언할 수 있음
* 지역변수와 전역변수가 있음
* 기본적으로 소문자로 시작되는 Camel Case 를 사용

```javascript
  var firstNumber:
  firstNumber = 10;
```

##### var, let, const - 전역변수

> ES6 이전에는 var 만 존재했으며 function-secoped로 인해 다른 언어들과 다른 문제가 있었음.

* var는 지역변수 개념으로 함수 범위에서 유효함
* var를 선언하지 않으면 자동으로 전역변수가 됨
* let과 const는 ES6 에서 등장한 block-scoped 변수 선언
* let은  값의 재할당이 가능하고 const는 불가능(immutable)
* const로 선언된 배열이나 객체의 경우 새로운 객체로 재할당하는 것은 안되고, 배열값의 변경/ 추가, 객체의 필드 변경등은 가능

다음은 var를 이용한 변수선언 예 입니다.

```javascript
var foo = 'foo1';
console.log(foo) // foo1

if (true) {
  var foo = 'foo2'
  console.log(foo) // foo2
}

console.log(foo) // foo2 @조건문에서 foo의 값을 재할당했기 때문에 바뀜
```

다음은 let과 const 예 

```javascript
let foo = 'foo1';
const bar = 'bar1';
console.log(foo) // foo1 @전역변수

if (true) {
  let foo = 'foo2'
  console.log(foo); // foo2 @지역변수
  console.log(bar); // bar1 @지역변수
}

console.log(foo); //foo1
bar = 'bar2' // error
```

##### hoistion
> 호이스팅은 끌어올리기라는 사전적 의미를 가지고 있습니다. 자바스크립트에서 모든 변수 선언은 호이스트 되고 함수의 경우 선언형식은 호이스팅 되며 변수에 할당된 형태는 호이스팅 되지 않습니다.

자바스크립트 변수에 있어 변수의 선언이 위치와 상관없이 최상위 레벨로 끌어올려진다고 이해할수 있습니다.

```javascript
if (true) {
  console.log(foo); //undefined
  var foo = 'foo1';
  console.log(foo); //foo1
}
```
* 일반적인 언어인 경우 foo 변수는 첫번째 출력문에서 선언되기 전 상태로 에러가 발생해야함
* 자바스크립트는 var foo가 호이스트 되어 변수는 선언되고 값이 할당되지 않는 상태가 됨

```javascript
var myVar;

function myVar() {
  ~~~
}
console.log(typeof(myVar)) //function
```
* 위 예제에서는 myVar라는 변수를 먼저 선언한 상태에서 동일 이름의 함수를 정의
- 함수 선언이 호이스팅 되어 myVar 변수에 할당

> 경우에 따라 호이스팅은 사소한 문제를 일으키지 않아 유용할 수 있으나 복잡한 코드에서는 오류 가능성이 높으므로 변수 선언시 var, let, const 등을 명확히 구분해서 사용하는 것이 좋다.

##### String 변수
일반적인 프로그램언어들은 문자열을 표현할때 큰따옴표("")를 사용하는데 반해 자바스크립트는 "",''를 모두 사용할 수 있다.

```javascript
var string;
string = "java Script"; // 혹은 'java Script'
```

<div class="divider"></div>

### 출력문

자바스크립트는 HTML 문서를 통해 웹브라우저에서 출력되므로 따로 출력문이 존재하다기 보다는 HTML 문서의 구성요소에 동적으로 출력하거나 웹브라우저의 경고창을 이용해 출력하는 형태가 출력문으로 볼 수 있습니다. 

물론 웹 브라우저의 콘솔창을 통해 메시지를 출력할 수도 있습니다.

1. HTML 문서에 출력

> HTML 문서에 출력하는 형태로 페이지가 모두 로딩된 다음에 실행하면 원래 있던 HTML 화면내용은 지워지게 됩니다.

다음 예제는 5+6의 연산결과를 웹브라우저에 출력합니다.

```HTML
<script>
document.write(5 + 6 );
</script>

<body>
  <h2>Hello World</h2>
</body>  

<!-- 위에 형식은 추천안함/ 로딩될 때 javascript를 불러와서 오래걸림 body 부분이 생략 될수 있음-->
```

2. HTML 문서의 특정부분에 출력
> HTML 문서의 특정요소를 찾아 해당 콘텐츠를 대체해 출력합니다. 자바스크립트에서 가장 보편적으로 HTML 문서를 동적으로 핸들링 하는 방법입니다.

다음 예제는 앞의 예제와 비슷하지만 기존 HTML 소스를 유지하고 부분적으로 변경됩니다.

```HTML
<script>
document.getElementById("result").innerHTML = 5 + 6;
</script>

<body>
<h2>Hello World</h2>
<div id="result"> 이 자리가 inerHTML 출력 결과물 11이 나오는 자리</div>
</body>
```

3. Alert 창을 이용한 출력
> 웹브라우저에서 오픈되는 조그만 경고창(alert)을 이용한 출력입니다. alert()을 사용합니다. 보통 프로그램에서 에러, 경고, 사용자 입력을 위해 많이 사용합니다.

```HTML
<script>
  alert(5 + 6)
</script>
```

4. 브라우저 콘솔창을 이용한 출력
> 자바스크립트 코드에서 진행상활을 출력하거나 개발을 위해 참고하기 위한 값들을 출력하기 위한 용도로 사용합니다.

```HTML
<script>
  console.log(5 + 6);
</script>
```

<div class="divider"></div>

### 연산자와 제어문
일반적인 프로그램언어와 같이 자바스크립트도 다양한 연산자와 if, for와 같은 제어문을 가지고 있습니다.

1. 연산자 
기본적으로 다른 프로그램 언어들과 유사합니다.

##### 비교 연산자

> 비교연산자의 결과는 기본적으로 true/false 입니다.

```
== 값이 같을 때
=== 값과 타입이 모두 같을 때
!= 값이 같지 않음
!== 값이나 타입이 같지 않음
> 크다
< 작다
>= 같거나 크다
<= 같거나 작다
? 3항연산 (조건)? 참인경우 수행: 거짓인 경우 수행
```

##### 논리 연산자

```
&& and 연산자
|| or 연산자
! NOT 연산자
```

2. 조건문 
C, 자바와 매우 유사합니다. if, else, swich 등이 있습니다.

if, else if

> 특정 조건이 참인 경우 수행되는 코드 블럭을 정의합니다. else와 결합해 조건 범위나 조건을 세분화하는 것이 가능하며 AND, OR 연산을 함께 사용할 수 있습니다.

```javascript
var score = 85;

if (score >= 90);
  console.log('A');
else if (scroe >= 80)
  console.log('B');
else if (scroe >= 70)
  console.log('C');
else
  console.log('F');
```
* score에 따라 해당 구간의 성적이 출력되도록 합니다.

##### swich
> 입력값에 따라 처리를 다르게 하는 경우 사용합니다. 내용적으로 if ~ else if 와 유사합니다.

```javascript
var level = 'B';

switch(level) {
  case 'A':
    console.log('VIP 등급'); break;
  case 'B':
    console.log('일반 등급'); break;
  default :
    console.log('등급없음'); break;
}
```

3. 반복문 
반복문 역시 C, 자바와 매우 유사합니다. for, while, forEach, for-in, for-of-for 등이 있습니다.

##### for
> 기본 구조는 시작, 종료조건, 증감식을 가지는 형태입니다. 다음 예제는 세개의 값을 가지는 배열을 선언하고 배열값을 모두 출력하는 예제입니다.

```javascript
const colors = ['red','blue','green'];
for (let i = 0; i< colors.length; i++) {
  console.log(colors[i])
}
```

##### while
> 조건이 성립하는 경우 계속 반복하는 구문입니다. 무한 루프가 되지 않도록 코드 중간에 조건을 반드시 변경해 주어야 합니다.

```javascript
const colors = ['red','blue','green'];
var i =0
while (colors[i] != null) {
  console.log(colors[i]);
  i++;
}
```

##### forEach
> ES5에서 사용가능하게 된 문법으로 배열이 모든 원소에 대해 특정 코드블럭을 수행할 수 있는 방법입니다. / 객체지향방법 = 객체들을 생산하고 그 생산한 객체들에게 일을 시키는 것

```javascript
const colors = ['red','blue','green'];
colors.forEach(function(value){
  console.log(value);
});
```

Es6 에서는 arrow 연산자를 통해 다으과 같이 간결하게 사용할수 있습니다.
```javascript
const colors = ['red','blue','green'];
colors.forEach( value => console.log(value));
```

##### for-in, for-of
> 최근 다른 언어들에 도입된 -in 형태의 구문입니다. 다만 -in의 경우 배열원소의 값에 접근할 수 없고 키 혹은 인덱스만 접근이 가능하므로 다른 언어에서의 -in과 같은 형태로 사용하려면 for-of를 사용해야 합니다.

```javascript
const colors = ['red','blue','green'];
for (var index in colors) {
  console.log(colors[index]);
}

for (var value of colos) {
  console.log(value);
}
```

###### for-in
- 객체의 모든 열거 가능한 속성에 대해 반복
- 즉, 배열 뿐만 아니라 일반적인 객체의 속성들을 모두 반복할 때도 사용 가능
- 모든 객체의 key(배열의 경우 인덱스)에 접근할 수 있지만, value에 접근할 수는 없음

###### for-of
- 반복 가능한(literable)객체의 값을 순환, 배열 이외 <em>문자열 데이터</em>(유니코드 이모지 포함 처리도 가능)
- ES6에 새로 추가된 MAP, SET에도 적용 가능
- Object를 대상으로 하지 않으며 객체의 속성을 순회하려면 for-in을 사용
- Object를 사용할 경우 object.key()로 키 값을 구해서 순회하면서 출력할 수 있음

<div class="divider"></div>

### 2022.10.17 게더 강의

```HTML

'할일' 버튼을 누르면 색이 바뀜

<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="\product.css">
	<title>DOM</title>
</head>
<body>
	<h3>할일 목록</h3>
	<ul>
		<li class="asdf">&#10003; 할일1</li>
		<li class="asdf">&#10003; 할일2</li>
		<li class="asdf">&#10003; 할일3</li>
		<li class="asdf">&#10003; 할일4</li>
		<li class="asdf">&#10003; 할일5</li>
	</ul>
	<script>
		let items = document.querySelectorAll(".asdf")
		console.log(items);

		function deleteItem() {
			this.style.textdecoration="line-through"
			this.style.color="#ccc"
		}

		for (let i = 0; i<items.length; i++) {
			items[i].addEventListener("click", deleteItem)
		}
  </script>
</body>
</html>
```