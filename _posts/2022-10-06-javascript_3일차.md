---
title: Javascript 3일차
updated: 2022-10-05 09:17
---
<div class="divider"></div>

### 화살표함수

```javascript
let sum = (a, b) => {
  return a + b;
}
// 밑에가 화살표함수
say("안녕하세요", (a, b) => a + b ,sayYes())
```

<div class="divider"></div>

### 엄격 모드
모던 자바스크립트에서 지원하는 모든 기능을 활성화하려면 스크립트 맨 위에 'use strict'를적어줘야 합니다.

<div class="divider"></div>

### 상호작용
1. prompt(question, [default])
프롬프트 창에 매개변수로 받은 question을 넣어 사용자에게 보여줍니다. ‘확인’ 버튼을 눌렀을 땐 사용자가 입력한 값을 반환해주고, ‘취소’ 버튼을 눌렀을 땐 null을 반환합니다.<br>
2. confirm(question)
컨펌 대화상자에 매개변수로 받은 question을 넣어 사용자에게 보여줍니다. 사용자가 ‘확인’ 버튼을 누르면 true를, 그 외의 경우는 false를 반환합니다.<br>
3. alert(message)
message가 담긴 얼럿 창을 보여줍니다. 세 함수는 모두 모달 창을 띄워주는데, 모달 창이 닫히기 전까지 코드 실행이 중지됩니다. 사
용자는 모달 창 외에 페이지에 있는 그 무엇과도 상호작용할 수 없습니다<br>

```javascript
let userName = prompt("이름을 알려주세요.", "영희");
let isTeaWanted = confirm("차 한 잔 드릴까요?");
alert( "방문객: " + userName ); // 영희
alert( "차 주문 여부: " + isTeaWanted ); // true
```
<div class="divider"></div>

### 연산자
자바스크립트는 아래와 같은 다양한 연산자를 제공합니다. 
1. 산술 연산자
사칙 연산에 관련된 연산자 * + - /와 나머지 연산자 %, 거듭제곱 연산자 **가 대표적인 산술 연산자에 속합니다. 이항 덧셈 연산자 +는 피연산자 중 하나가 문자열일 때 나머지 하나를 문자형으로 바꾸고 두
문자열을 연결합니다. <br>
```javascript
alert( '1' + 2 ); // '12', 문자열
alert( 1 + '2' ); // '12', 문자열\
```

2. 할당 연산자
a = b 형태의 할당 연산자와 a *= 2 형태의 복합 할당 연산자가 있습니다.<br>

3. 비트 연산자
비트 연산자는 인수를 32비트 정수로 변환하여 이진 연산을 수행합니다. 자세한 내용은 docs에서 볼 수 있습니다. <br>
4. 조건부 연산자
조건부 연산자는 자바스크립트 연산자 중 유일하게 매개변수가 3개인 연산자입니다. cond ?
resultA : resultB와 같은 형태로 사용하고, cond가 truthy면 resultA를, 아니면 resultB를 반환합니다. <br>
5. 논리 연산자
AND 연산자 &&와 OR 연산자 ||은 단락 평가를 수행하고, 평가가 멈춘 시점의 값을 반환합니다(꼭 true나 false일 필요는 없습니다). NOT 연산자 !는 피연산자의 자료형을 불린형으로 바꾼 후 그 역을 반환합니다.<br>
6. null 병합 연산자
null 병합 연산자 ??는 피연산자 중 실제 값이 정의된 피연산자를 찾는 데 쓰입니다. a가 null이나 undefined가 아니면 a ?? b의 평가 결과는 a이고, a가 null이나 undefined이면 a?? b의 평가 결과는 b가 됩니다.<br> 
7. 비교 연산자
동등 연산자 ==는 형이 다른 값끼리 비교할 때 피연산자의 자료형을 숫자형으로 바꾼 후 비교를 진행합니다. null과 undefined는 자기끼리 비교할 땐 참을 반환하지만 다른 자료형과 비교할 땐 거짓을 반환합니다. <br>
```javascript

alert( 0 == false ); // true
alert( 0 == '' ); // true
```
기타 비교 연산자들 < > <= >= 역시 피연산자의 자료형을 숫자형으로 바꾼 후 비교를 진행합니다. <br>

8. 일치 연산자 ===는 피연산자의 형을 변환하지 않습니다. 형이 다르면 무조건 다르다고 평가합니다. null과 undefined는 특별한 값입니다. 두 값을 == 연산자로 비교하면 true를 반환하지만, 다
른 값과 비교하면 무조건 false를 반환합니다. 크고 작음을 비교하는 연산자의 피연산자로 문자열이 들어오면 글자 단위로 크기 비교가 이뤄
집니다. 다른 타입의 값이 들어오면 숫자형으로 형 변환한 후 비교를 진행합니다. <br>

9. 기타 연산자
쉼표 연산자 등의 기타 연산자도 있습니다.
자세한 내용은 기본 연산자와 수학, 비교 연산자, 논리 연산자, null 병합 연산자 '??'에서 살
펴보시기 바랍니다.<br>

<div class="divider"></div>

### 반복문
```javascript

while, do-while, for 문은 아래와 같이 작성할 수 있습니다. // 1
while (condition) {
 ...
}
// 2
do {
 ...
} while (condition);
// 3
for(let i = 0; i < 10; i++) {
 ...
}
```
for(let...) 안쪽에 선언한 변수는 오직 반복문 내에서만 사용할 수 있습니다. let을 생략하고 기존에 선언되어있는 변수를 사용하는 것도 가능합니다.<br>

<div class="divider"></div>

### switch문
'switch’문은 if문을 사용해 재작성할 수 있습니다. 'switch’문은 조건을 확인할 때 내부적으로
일치 연산자 ===를 사용해 비교를 진행합니다. <br>예시:
```javascript

let age = prompt('나이를 알려주세요.', 18);
switch (age) {
 case 18:
 alert("Won't work"); // prompt 함수는 항상 문자열을 반환하므로, 이 case문엔 절대
도달할 수 없습니다.
 break;
 case "18":
 alert("낭랑 18세이시군요!");
 break;
 default:
 alert("어떤 case문에도 해당하지 않습니다.");
}
```

<div class="divider"></div>

### 함수

세 가지 방법으로 함수를 만들 수 있습니다. 
1. 함수 선언문: 주요 코드 흐름을 차지하는 방식<br>

```javascript
function sum(a, b) {
 let result = a + b;
 return result;
}
```

2. 함수 표현식: 표현식 형태로 선언된 함수
```javascript
let sum = function(a, b) {
 let result = a + b;
 return result;
};
```

3. 화살표 함수:

```javascript
// 화살표(=>) 우측엔 표현식이 있음
let sum = (a, b) => a + b;
// 대괄호{ ... }를 사용하면 본문에 여러 줄의 코드를 작성할 수 있음. return문이 꼭 있어야
함.
let sum = (a, b) => {
 // ...
 return a + b;
}
// 인수가 없는 경우
let sayHi = () => alert("Hello");
// 인수가 하나인 경우
let double = n => n * 2;
```
함수는 지역 변수를 가질 수 있습니다. 지역 변수는 함수의 본문에 선언된 변수로, 함수 내부에서만 접근할 수 있습니다. 매개변수에 기본값을 설정할 수 있습니다. 문법은 다음과 같습니다. <br>

<em>function sum(a = 1, b = 2) {...}</em><br>

함수는 항상 무언가를 반환합니다. return문이 없는 경우는 undefined를 반환합니다. <br><br>
자세한 내용은 함수와 화살표 함수 기본에서 살펴보시기 바랍니다.

<div class="divider"></div>

### 객체

```javascript
// 배열
let array = [];
let array = new Array();

let obj = {};

// 딕셔너리
obj = {key1:"value1", key2:"value2"}

obj[key1]
```

```javascript
let obj = {윤성현:"오늘휴가씀"}

alert(obj[윤성현]);
```
