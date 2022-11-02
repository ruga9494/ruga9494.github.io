---
title: Javascript 11일차
updated: 2022-11-02 21:12
---

### 부수효과 // Pure Function

> 같은 입력값이 주어졌을 때, 언제나 같은 결과값을 리턴한다.
사이드 이펙트(Side Effect)를 만들지 않는다. (= 외부에서 선언된 상태(state)를 수정하지 않는다.)

예시문제

```javascript
const weeks = ['일','월','화','수','목','금','토']

const getNextWeek = () => {
  let widx = -1;
  return () => {
    widx += 1; 
    if (widx >= weeks.length) widx = 0;
    return `${weeks[widx]요일}` ;
  }
}

const nextWeek = getNextWeek(); // 함수를 한번만 호출했기 때문에 widx = -1은 한번만 호출 한 것으로 생각 해야함
console.log(nextWeek()); 
// 일 > widx = -1 이기 때문에 return으로 들어간 후 0이 되서 일요일을 호출
console.log(nextWeek()); // 월
// 일 > widx = 0 이기 때문에 return으로 들어간 후 1이 되서 월요일을 호출
console.log(nextWeek()); // 화
// 일 > widx = 1 이기 때문에 return으로 들어간 후 2가 되서 화요일을 호출
console.log(nextWeek()); // 수
// 일 > widx = 2 이기 때문에 return으로 들어간 후 3이 되서 수요일을 호출
console.log(nextWeek()); // 목
// 일 > widx = 3 이기 때문에 return으로 들어간 후 4가 되서 목요일을 호출
console.log(nextWeek()); // 금
// 일 > widx = 4 이기 때문에 return으로 들어간 후 5가 되서 금요일을 호출
console.log(nextWeek()); // 토
// 일 > widx = 5 이기 때문에 return으로 들어간 후 6이 되서 토요일을 호출

```

> Side Effect를 막기 위해서 함수 자체적으로 작동함 widx가 외부로부터 영향을 받지 않음

<div class="divider"></div>

### reduce 사용하기

> 메서드는 배열의 각 요소에 대해 주어진 **리듀서**(reducer) 함수를 실행하고, 하나의 결과값을 반환합니다.

```javascript
const arr = [1,2,3,4,5];

const f1 = v => v**2
const f2 = v => Math.sqrt(v) // 제곱근
const f3 = v => v**3

const result = [f1,f2,f3].reduce((pre, f) => pre.map(f), arr);
console.log(result);

// 아래는 result 안에 값들이 순서대로 작동하는 것을 나타냄
/*        pre            f         map
0 ==>  [1,2,3,4,5]       f1       [1,2,3,4,5].map(v => v ** 2)
1 ==>  [1,4,9,16,25]     f2       [1,4,9,16,25].map(v =>  Math.sqrt(v))
2 ==>  [1,2,3,4,5]       f3       [1,2,3,4,5].map(v => v ** 3)
result = [1,8,27,64,125]      
*/

```
키워드
> const result = [f1,f2,f3].reduce((pre, f) => pre.map(f), arr);

<div class="divider"></div>

### Map 함수 사용법 

* 아직어렵고 이해 안 되어있음

* 중요
> map() 메서드는 배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.

```javascript
const hrTeam = {id:1, dname:'인사팀'}
const devTeam = {id:2, dname: '개발팀'};
const depts = [hrTeam, devTeam];

const hong = {id:1, name:'Hong', dept:1};
const Kim = {id:2, name:'Kim', dept:2};
const emps = [hong, Kim, {id:3, name:'Park', dept:2}, {id:4, name:'choi', dept:2}];

const deptMap = new Map(depts.map( d => [d.id, d]))
// Map(2) { 1 => { id: 1, dname: '인사팀' }, 2 => { id: 2, dname: '개발팀' } }

const empMap = new Map(emps.map( e =>{
  const dept = deptmap.get(e.dept) // e의 dept를 deptmap 에서 똑같은 값을 찾아서 채운다. 이말이야
  return [e.id, {...e, dept}];
}))
/* Map(4) {
  1 => { id: 1, name: 'Hong', dept: { id: 1, dname: '인사팀' } }, 
  dept는 월래 1 인데 deptMap에서 1이랑 empmap의 dapt의 1이랑 매칭시켜 치환 해줬다고 생각하면 됨 밑에것도
  2 => { id: 2, name: 'Kim', dept: { id: 2, dname: '개발팀' } },
  3 => { id: 3, name: 'Park', dept: { id: 2, dname: '개발팀' } },
  4 => { id: 4, name: 'choi', dept: { id: 2, dname: '개발팀' } }
*/

const result = [...empMap]
  .filter(([_, emp]) => emp.dept.id ===2) //?
  .map(([_, emp]) => emp.name); //? 질문해야함

console.log(result);
//[ 'Kim', 'Park', 'choi' ] 이름값만 뽑아냄

```

<div class="divider"></div>

### Set , includes 함수 응용하기

> Set 객체는 자료형에 관계 없이 원시 값과 객체 참조 모두 유일한 값을 저장할 수 있습니다.

> includes() 메서드는 배열이 특정 요소를 포함하고 있는지 판별합니다.


```javascript

const A = [1,2,3,4,5,3];
const B = [1,22,3,44,5];
const C = [11,222,3,4,555];

const intersect = (arr1, arr2) => new Set(arr1.filter(a => arr2.includes(a)));
// new set으로 중복값을 제거 해준다. 
// filter를 한다 뭘로? arr2이 include된 값으로 필터를 해준다. (교집합)
console.log(intersect(A,B))// 1, 3, 5
console.log(intersect(A,B))// 3, 4

const diff = (arr1, arr2) => new Set(arr1.filter(a => !arr2.includes(a)));
// new set으로 중복값 제거 후에 arr2랑 겹치지 않는 값을 필터링 한다. (차집합)
console.log(diff(A, B)); // 2, 4
console.log(diff(B, A)); // 22, 44
console.log(diff(A, C)); // 1, 2, 5
console.log(diff(B, C)); // 1, 22, 44, 5

const union = (arr1, arr2) => new Set([...arr1, ...arr2]);
/*
new set으로 중복값 제거 후 arr1을 ...을 활용해 다 리스트를 펼쳐준다. 
마찬가지로 arr2를 ...을 활용해 리스트를 펼치고 한 리스트안에 담는다.
*/
console.log(union(A,B)); //1, 2, 3, 4, 5, 22, 44
console.log(union(A,C)); //1, 2, 3, 4, 5, 11, 222, 555

```

야팔.. 왜이렇게 어렵냐