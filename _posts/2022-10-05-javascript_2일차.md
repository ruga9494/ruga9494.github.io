---
title: Javascript 2일차
updated: 2022-10-04 21:32
---

### 자료형

null

undefined

값이 할당되지 않은 것

```javascript
let age;

alert(age);
```

###  자바스크립트
객체 개체 객체지향 - 자료구조형 (서로 별개이다.)
{"":"", "":""} -> 딕셔너리랑 비슷하다.

xml -> json ->restapi
규약

j : javascript

여러언어 여러 통신 자료전달

<div class="divider"></div>

파이썬 어레이 리스트
["a","b"]
튜플
("a","b")
딕셔너리 맵 해시맵(자바)
{"a":"A","b":"B"}

판다스
데이터 프레임워크

<div class="divider"></div>

자료형을 확인하는 방법
 - javascript에서 'typeof()' 라는 것을 사용함
 - python은 'type()'을 사용함

### 단축키 

ctrl D -동일한 값 커서 넣어주기
arlt shift I

아주 오래전에 만들어진 규칙이었기 때문에 
하위 호환성 유지

<div class="divider"></div>

숫자형 – 정수, 부동 소수점 숫자 등의 숫자를 나타낼 때 사용합니다. 정수의 한계는 ±253입니다. <br>
bigint – 길이 제약 없이 정수를 나타낼 수 있습니다. <br>
문자형 – 빈 문자열이나 글자들로 이뤄진 문자열을 나타낼 때 사용합니다. 단일 문자를 나타내는 별도의 자료형은 없습니다. <br>
불린형 – true, false를 나타낼 때 사용합니다. <br>
null – null 값만을 위한 독립 자료형입니다. null은 알 수 없는 값을 나타냅니다. <br>
undefined – undefined 값만을 위한 독립 자료형입니다. undefined는 할당되지 않은 값을나타냅니다. <br>
객체형 – 복잡한 데이터 구조를 표현할 때 사용합니다. <br>
심볼형 – 객체의 고유 식별자를 만들 때 사용합니다. typeof 연산자는 피연산자의 자료형을 알려줍니다.<br>

<div class="divider"></div>


### alert prompt conform 상호작용

창안에 창을 넣는 기능
iframe 지양

모달로 대체

1. alert
2. prompt
3. confirm

형변환 

자바스크립트 동적타입핑 언어 자동자료형변환이 되는 언어

### 프롬프트(prompt)
result = prompt(title);

```javascript
let name = prompt("이름을 입력해주세요", "문창일");
alert(`제이름은 ${name} 입니다.`);
```

<em>python의 input과 느낌이 비슷하다.</em>

<div class="divider"></div>

### 콘필름(Confirm)

```javascript
let isBoss = confirm("당신이 주인인가요?");
alert( isBoss ); // 확인 버튼을 눌렀다면 true가 출력됩니다.
```

<div class="divider"></div>

### 타입확인

```javascript
alert(typeof undefined); // "undefined"
alert(typeof 0); // "number"
alert(typeof 10n); // "bigint"
alert(typeof true); // "boolean"
alert(typeof "foo"); // "string"
alert(typeof Symbol("id")); // "symbol"
alert(typeof Math); // "object" (1) 내장함수이다
alert(typeof null); // "object" (2)
alert(typeof alert);// "function" (3)
```
### 형변환

```javascript
String(value): // 문자형
Number(value): // 숫자형
Boolean(value): // 불린형
```


- html은 폼을 통해서 받는다. 

```
<form>
  <input type="text">
</form>
```

- boolean형

```javascript
alert( Boolean(1) ); // 숫자 1(true)
alert( Boolean(0) ); // 숫자 0(false)
alert( Boolean("hello") ); // 문자열(true)
alert( Boolean("") ); // 빈 문자열(false)
```

주의: 자바스크립트의 문자열 "0"은 True입니다. <br>
PHP 등의 일부 언어에서 문자열 "0"을 False로 취급합니다. <br>
그러나 자바스크립트에서는 비어 있지 않은 문자열은 언제나 True입니다. <br>

<div class="divider"></div>

### 연산자 
1. 단항 한개의 항목 <br>
2. 이항 2개의 항목 <br>
3. 삼항연산자 <br>
4. 피연산자 대상이 되는 항목 <br>
5. 인수 <br>
6. 할당연산자 <br>
 - 값을 할당하는 연산자
 - 왼쪽 = 오른쪽
 ```javascript
 let a = 1;
 let b = 2;
 let c = 3 - (1 = b + 1);

 alert(a); //3
 alert(c); //0
 ```


나머지 %  <br>
거듭제곱 ** <br>
덧셈 + (문자열연결에도 쓰임)<br>
   상식) 
   1. php는 문자열 연결을 "."으로 함      
   2. javascript에서는 숫자열 + 문자열을 할 경우에는 문자열로 바꾼뒤에 붙여준다. (형변환 후 더함)<br>

<div class="divider"></div>

### 체이닝

파이썬 체이닝
객체.객체.객체

자바스크립트 체이닝

```javascript
let a,b,c;

a = b = c = 2 + 2;
alert(a); //4
alert(b); //4
alert(c); //4
```

<div class="divider"></div>

### 복합할당연산자

1. +=
2. -=
3. *=

프로그램을 짜다 보면, 변수에 연산자를 적용하고 그 결과를 같은 변수에 저장해야 하는 경우

```javascript
let n = 2;
n = n + 5;
n = n * 2;

let n = 2;
n += 5; // n은 7이 됩니다(n = n + 5와 동일).
n *= 2; // n은 14가 됩니다(n = n * 2와 동일)
```

### 증가감소연산자

주로 for문에서 씀

c 스타일의 포문
```javascript
for (i=0; i<변수.lenght;, i++){
  
}
for ($i=0;$i<count(변수);, i++){

}
```

후위형 postfix
전위형 prefix

더한 다음에 처음 것을 넣어주느냐 -> ? 먼소리

### 비트와이즈연산자
1. 비트 AND ( "&" )
2. 비트 OR ( "\" )
3. 비트 XOR ( ^ )
4. 비트 NOT ( ~ )
5. 왼쪽 시프트(LEFT SHIFT) ( << )
6. 오른쪽 시프트(RIGHT SHIFT) ( >> )
7. 부호 없는 오른쪽 시프트(ZERO-FILL RIGHT SHIFT) ( >>> )

### 쉼표 연산자 
,는 여러 표현식을 코드 한 줄에서 평가할 수 있게 해줍니다. 이때 표현식 각각
이 모두 평가되지만, 마지막 표현식의 평가 결과만 반환되는 점에 유의해야 합니다. 

```javascript

let a = (1 + 2, 3 + 4);
alert( a ); // 7 (3 + 4의 결과)
```

여러 동작을 하나의 줄에서 처리하려는 복잡한 구조에서 이를 사용합니다. 아래와 같이 말이죠. // 한 줄에서 세 개의 연산이 수행됨
```javascript

for (a = 1, b = 3, c = a * b; a < 10; a++) {

}
```

### 비교연산자
1. ">"
2. "<"
3. "==" 동등연산자
4. "===" 타입까지 같은 것 / 엄격하다 엄격한 일치 (자료형까지 같아야함)
5. "!="

자바스크립트에서만 일어나는 기이한 현상 반직관

##### 문자열 비교
 - 사전편집(lexicographical) 알파벳순
 - 정확히는 사전 순이 아니라 '유니코드순'이다.
 ```javascript
  alert('Z' > 'A'); //True
 ```

##### 다른 형을 가진 값 간의 비교(타입변환)

```javascript
let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!
```

##### null이나 undefined와 비교하기


```javascript
alert(null == undefined);
alert(null === undefined);
```

##### 조건부 연산자

```javascript
let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');
if (year == 2015) alert( '정답입니다!' );
```

삼항연산자

```javascript

if (a==true) {

} else if {

} else {

}
```

조건부 연산자는 물음표?로 표시합니다. 피연산자가 세 개이기 때문에 조건부 연산자를 '삼항(ternary) 연산자’라고 부르는 사람도 있습니다. 참고로 자바스크립트에서 피연산자가 3개나받는 연산자는 조건부 연산자가 유일합니다.

```javascript
let age = prompt('나이를 입력해주세요.', 18);
let message = (age < 3) ? '아기야 안녕?' :
 (age < 18) ? '안녕!' :
 (age < 100) ? '환영합니다!' :
 '나이가 아주 많으시거나, 나이가 아닌 값을 입력 하셨군요!';
```

 - ? : 삼항연산자 if 문을 처리할 수 있다.

##### 논리연산자
 "||"(or), "&&"(AND), "!"(NOT)

 ```javascript
let hour = 0
if ((hour < 10) || (hour >18)){
  alert("hh");
}
```

##### nullish 병합연산자 ??
 - 스펙에 추가된지 얼마 안 된 문법이다. 구식 브라우저는 폴리필이 필요함
 ECMA2022  << 요게 스펙

<div class="divider"></div>

### 반복문
 - while문

a =0;
while (조건) {
  a += 1
}

 - for문
for (초기값; 조건; 증감) {

}

```javascript
let list = ['a','b'];
    for (i=0; i<list.length; i++) {
      console.log(`${i}번째 항목입니다. 값은 ${list[i]}`);
    }
```

```html
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
  <table>
    <tr>
      <td id="name"></td>
      <td id="age"></td>
    </tr>
  </table>

  <script>
    let column1 = [
    "홍길동",
    "세종대왕",
    "이순신",
    "홍길동",
    "세종대왕",
    "이순신",
    ];
    let column2 = [33, 44, 55, 33, 44, 55];

    for (i = 0; i < column1.length; i++) {
      console.log(`${i}번째 항목입니다.값은 ${column1[i]}`);
    }

    for (let i =0; i < 3; i ++) {
      for (let j =0; j< 3; j++) {
        if (j==1) {
          alert(`${i} and ${j}`);
          break
        }
      }
      break
      alert(`${i} and ${j}`);
    }
  </script>
</body>
</html>
```

<div class="divider"></div>

### 조건문 if 문
```javascript
let a = 2 + 2;
switch (a) {
 case 3:
 alert( '비교하려는 값보다 작습니다.' );
 case 4:
 alert( '비교하려는 값과 일치합니다.' );
 case 5:
 alert( '비교하려는 값보다 큽니다.' );
 default:
 alert( "어떤 값인지 파악이 되지 않습니다." );
}
```

<div class="divider"></div>

### 함수

function showmessage(매개변수)

```javascript
function showMessage(name, age) {
  let 소개 = `이름은${name} 입니다. 나이는 ${age}입니다`
  return 소개 
}

let 소개 = showMessage("문창일", 29);
```

```javascript
function checkAge(age) {
 if (age >= 18) {
 return true;
 } else {
 return confirm('보호자의 동의를 받으셨나요?');
 }
}
let age = prompt('나이를 알려주세요', 18);
if ( checkAge(age) ) {
 alert( '접속 허용' );
} else {
 alert( '접속 차단' );
}
```

```javascript
function checkname(name) {
      switch(name) {
        case "문창일":
        console.log(`안녕하세요 ${name}님`)
        break
        case "도둑":
        console.log(`저리가세요 ${name}님`)
        break
        default:
        console.log(`안녕하세요 ${name}님`)
      }
    }

    let name1 = prompt('이름을 알려주세요', "문창일");
    checkname(name1)
```

<div class="divider"></div>

파이썬 - 람다함수
자바스크립트 - 콜백함수 (함수가 함수를 부르는?)


#### 콜백함수 예시
```javascript
function ask(question, yes, no){
  if (confirm(question)) {
    yes()
  }else{
    no();
  } 
}
function showOk() {
  alert("동의하셨습니다.");
}
function showCancel() {
  alert("취소 버튼을 누르셨습니다.");
}

ask("동의하시겠습니까?", showOk, showCancel); //콜백함수


ask(
  "동의하시겠습니까?"
  function() { alert("동의하셨습니다."); },
  function() { alert("취소 버튼을 누르셨습니다."); }
);
```

#### 함수 표현식
```javascript
let sum = function(a, b) {
 return a + b;
};
```

#### 함수 선언문
```javascript

sayHi("John"); // Hello, John
function sayHi(name) {
 alert( `Hello, ${name}` );
}
```

### 함수 표현식과 선언문의 차이
 - 함수를 변수에 담는 것은 변수를 먼저 인식 해야 함수가 작동이 가능 (함수표현식)
 - 함수를 선언할 경우 위치와 상관없이 javascript가 작동될 때, 함수가 선언이 됨 (함수선언문)


#### 화살표함수

함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법이 있습니다. 바로 화살표 함수(arrow function)를 사용하는 것입니다. 화살표 함수라는 이름은 문법의 생김새를 차용해 지어졌습니다. <br>

이렇게 코드를 작성하면 인자 arg1..argN를 받는 함수 func이 만들어집니다. 함수 func는화살표(=>) 우측의 표현식(expression)을 평가하고, 평가 결과를 반환합니다. 아래 함수의 축약 버전이라고 할 수 있죠.
```javascript
let func = function(arg1, arg2, ...argN) {
 return expression;
};
```
좀 더 구체적인 예시를 살펴봅시다.
```javascript
let sum = (a, b) => a + b;
```
/* 위 화살표 함수는 아래 함수의 축약 버전입니다.