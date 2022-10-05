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
1. 비트 AND ( & )
2. 비트 OR ( | )
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

alert(null == undefined);<br>
alert(null === undefined);

```javascript
alert(null == undefined);
alert(null === undefined);
```

#### 조건부 연산자

let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');<br>
if (year == 2015) alert( '정답입니다!' );

```javascript
let year = prompt('ECMAScript-2015 명세는 몇 년도에 출판되었을까요?', '');
if (year == 2015) alert( '정답입니다!' );
```

삼항연산자

```javascript

if () {

} else {

} else {

} else {

}
```