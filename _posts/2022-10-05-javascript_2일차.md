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
``` html
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
단항 한개의 항목 <br>
이항 2개의 항목 <br>
삼항연산자 <br>
피연산자 대상이 되는 항목 <br>
인수 <br>

나머지 %  <br>
거듭제곱 ** <br>
덧셈 + (문자열연결에도 쓰임)<br>
   상식) 1. php는 문자열 연결을 "."으로 함 <br>
         2. javascript에서는 숫자열 + 문자열을 할 경우에는 문자열로 바꾼뒤에 붙여준다. (형변환 후 더함)<br>

