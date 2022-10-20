---
title: Javascript 8일차
updated: 2022-10-18 09:14
---

<div class="divider"></div>

### 배열과 자료구조

기본적인 개념은 다른언어와 동일하지만 <b>정의하거나 사용하는 형태</b>는 다소 차이가 있습니다.

1. 배열 
배열의 선언은 [] 나 new Array()로 생성하고 크기의 제약이 없으며 하나의 배열에 <em>서로 다른 타입</em>의 변수가 들어갈 수 있습니다.

다음은 다양한 배열 선언 예 입니다.

```javascript
var emptyArray = [];
var nambers1 = [10,30,50,70,90];
var numbers2 = new Array(20,40,60,80,100);
var mixedArr = ['a',1,'b',2,new Date(),"Today"]; //함수도 가능

console.log(numbers2[2])
console.log(mixedArr[4])
```
아직 자바스크립트 객체를 배우기 전이지만 배열에 <b>자바스크립트 객체</b>를 넣을 수 있습니다. 이를 이용하면 JSON 데이터의 집하을 만들 수 있으며 서버와의 데이터 교환에 사용할 수 있는 구조가 됩니다.

```javascript
var objArr = [
  {
    "id":20192010,
    "name":"홍길동"
    "dept":"컴퓨터공학과"
  }
  {
    "id":20192011,
    "name":"김사랑"
    "dept":"경영학과"
  }
  {
    "id":20192012,
    "name":"강동수"
    "dept":"전자공학과"
  }
]
```

배열의 주요 메서드
> 배열 데이터를 다루기 위한 다양한 메서드(함수)가 제공되고 있습니다. 각각에 대한 구체적인 동작은 예제를 통해 확인하기 바랍니다.

##### 데이터 변경
- push(): 배열의 끝에 값을 추가
- pop(): 배열 마지막 값을 제거
- shift(): 배열 데이터를 왼쪽으로 하나씩 밀어 맨앞 값을 제거
- splice(): 배열값을 추가하거나 제거해서 반환
- reverse(): 배열을 역순으로 재배치
- sort(): 배열 데이터를 정렬

##### 배열의 일부를 반환
- concat(): 두개의 배열을 합침
- join(): 배열 데이터 사이에 원하는 문자열을 넣어 구분자로 사용
- slice(): 배열의 일부을 지정해서 가져옴

##### 데이터 순회
- map(): 모든 배열 데이터마다 반복처리가 필요한 경우 사용
- filter(): 특정 조건을 만족하는 데이터만 처리할 경우 사용
- reduce(): 모든 데이터를 순회하면서 누적 연산이 필요한 경우

2. Map, Set
ES6에서 새롭게 추가된 자료 구조입니다. 기존 자바스크립트는 배열 이외의 자료구조가 따로 없었으나 이제 다른 언어들 처럼 다양한 자료구조를 사용할 수 있게 되었습니다.

Map과 Set의 기본적인 개념은 기존언어들과 동일하다.

##### Map
> Map은 new Map()으로 선언하고 map.set()을 이용해 키와 값을 추가합니다.

자바스크립트의 Map은 Key:value 쌍으로 구성된 Object와 비슷한 구조로 볼 수 있지만 다음과 같은 차이가 있습니다.

- Object는 키는 문자열이며, Map의 키는 모든 값을 가질 수 있다.
- Objext는 크기를 수동으로 추적해야하지만, Map은 크기를 쉽게 얻을 수 있다.
- Map은 삽입된 순서대로 반복된다.
- 객체(Object)에는 prototype이 있어 Map에 기본 키들이 있다.

> 언제 Object 혹은 Map을 사용할까?
> 실행 시점까지 키를 알수 없고, 모든 키가 동일한 type이며 모든 값들이 동일한 type일 경우에는 object를 대신해서 map을 사용하는 것이 좋습니다. 만일 각 개별 요소에 대해 적용해야 하는 로직이 있다면 object를 사용하길 권장합니다.

다음은 여러 유형의 Map 사용 예 입니다.

```javascript
const map = new Map();
map.set("2019101","홍길동");
map.set("2019102","김사랑");
map.set("2019103","강동수");

console.log(map.get("2019101"));
map.delete("201903")
console.log(map.has("2019103"));

map.forEach((value, key) => console.log(key+" , "+value));

for(let item of map) {
  console.log(item[0]+" , "+item[1]);
}
for(let [key, value] of map) {
  console.log(key+" , "+value);
}

const keys = map.key();
for(let key of keys) {
  console.log(map.get(key));
}
```

- forEach의 인자는 valu,key,map object 입니다.
- for-of 형태를 사용하는 경우 배열로 키(0),키(1)가 전달됩니다.
- map.keys()로 키값의 집합인 Mapliterator 객체를 받아 for-of를 이용합니다.

##### Set
> Set은 중복된 값을 허용하지 않고 입력된 순서에 따라 데이터를 저장하는 자료구조입니다. set.add()를 이용해 데이터를 추가할 수 있꼬 데이터 관리를 위한 메서드가 제공됩니다.

배열과 유사하지만 다음과 같은 차이가 있다.
- indexOf()를 사용하여 배열내에 특정 요소가 존재하는지 확인하는 것은 느리다.
- 배열에선 해당 요소를 배열에서 잘라내야 하는 반면 Set은 삭제 기능을 제공한다.
- NaN은 배열에서 indexOf메서드로 찿ㅈ을 수 없다.
- Set객체는 값의 유일성을 보장하기 때문에 직접 요소의 중복성을 확인할 필요가 없다.

```javascript
const set = new Set();
set.add("홍길동");
set.add("김사랑");
set.add("강동수");

set.delete("강동수")
console.log(set.has("강동수"));

set.forEach((value) => console.log(value));

for(let item of set) {
  console.log(item);
}
```

Set은 배열로 배열은 Set으로 변경이 가능합니다. 배열에서 Set으로 변환될 경우 중복된 값은 제거됩니다.

```javascript
let arr = Array.from(set);

let newSet = new set([1,2,3,4,3]);
```

### 함수(Function)
함수의 개념은 대부분의 프로그램 언어에서 존재하지만 특히 자바스크립트는 함수를 변수에 할당 할수 있으며 인자로 함수를 전달하거나 콜백함수를 구현하는 형태등 다양한 함수 활용을 보여주고 있습니다.

##### 함수선언
> 기본적으로 function 키워드로 선언하며 인자를 가질 수 있습ㄴ디ㅏ. 자바스크립트는 타입을 명시하지 않기 때문에 리턴 값의 유무와 상관없이 함수 선언부에 리턴 데이터에 대한 선언은 없습니다. 필요시 함수 바디에서 return문을 사용해 값을 반환하면 됩니다.

- 인자의 매개변수 역시 타입없이 갯수에 따라 변수명을 나열
- 함수안에 사용되는 변수는 block-scoped 인 let 이나 const 사용을 권장 // 지역변수
- 함수안에 또다른 함수를 정의할 수 있습니다.

```javascript
function calc(a,b) {
  let sum1 = a + b ;
  sum2 = a+b;
    return sum1;
}

console.log(calc(20, 30)); // 50
console.log(sum2); // 50
console.log(sum1); // Error -not defined
```

##### First Class Object
> 자바스크립트에서 함수는 일급객체라고도 하며 다음과 같은 조건을 만족하는 객체를 말합니다.

- 변수나 데이터 구조안에 담을 수 있다.
- 파라미터로 전달 할 수 있다.
- 반환값(return value)으로 사용할 수 있다.
- 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다.
- 동적으로 속성 할당이 가능하다.

##### 익명함수(Anonymous Function)
> 익명함수는 이름이 없는 함수로 변수에 함수를 구현하거나 함수를 리턴하는 형태가 가능하며 이를 사용하며 소위 콜백함수의 구현이 가능해 집니다.

```javascript
var calc1 = function(a,b) {
  return a+b;
}

function calc2(func) {
  console.log(func(20,30));
}

console.log(calc1(20,30));
calc2(calc1);
```

##### 콜백함수(Callback Function)
> 자바스크립트에서 콜백함수는 특히 이벤트 처리에 많이 사용됩니다. 특정 UI에서 이벤트가 발생되었을때, 처리될 코드를 익명함수에 넣고 콜백되어 처리될 수 있도록 하는 형식입니다.

다음은 제곱을 구하는 함수에서 콜백함수를 호출하는 예 입니다. 콜백함수의 기능은 단순히 값을 콘솔에 출력하고 있습니다. setTimeout 함수는 일정시간 후에 동작을 정의합니다. 여기서는 200밀리초 이후 callback을 호출하며 파라미터로 제곱값을 전달 하게 되어 있습니다.

```javascript
function square(x, callback) {
  setTimeout(callback, 200, x*x)
}

square(2, function(number){
  console.log(number);
});

```

##### 자료구조의 값에 함수 사용
> 앞에서 언급한 것처럼 함수를 객체의 속성으로 사용할 수 잇으며 Map의 Value 혹은 배열의 원소로도 사용할 수 있습니다.

```javascript
// 배열원소로 함수 선언
let funcArr = [function() {console.log("v1")}, "v2"];

// 맵원소로 함수 선언
let mapArr = new Map();
mapArr.set("calcFunc",function(n1,n2) {return n1*n2});

// 객체의 속성으로 함수 선언
let student = {
  'id':2019131,
  'name':'홍길동'
  'score':function() {
    alert('A+');
  }
}

console.log(funcArr[0]);
console.log(mapArr.get("calcFunc")(20,10));
console.log(student.id);
studdent.score();
```

### 객체와 클래스