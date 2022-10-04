---
title: Javascript 1일차
updated: 2022-10-04 17:42
---
<div class="divider"></div>

### 자바스크립트란?
 >> 특징 웹 생동감을 불어넣는다. 동적인 페이지

<div class="divider"></div>

### 자바스크립트 엔진, 가상머신
 - 크롬브라우저 오페라브라우저 - v8
 - 파이어폭스 스파이더몽키
 - 익스플로러 트라이던트 샤크라
 - 엣지 샤크라코어 
 - 사파리 시쿼럴피쉬

<div class="divider"></div>

### 자바스크립트 엔진의 역할
 >> 파싱(parsing)
 >> 언어 종류
 >> c언어 어렵다
 >> 가비지컬렉션 (쓰레기 메모리를 만드는 듯?)]

<div class="divider"></div>

### 파싱(parsing)이란?
 >> v8 스크립트를 읽어서 기계어로 변환 (컴파일)

<div class="divider"></div>

### 브라우저에서 할수 있는 일
#### 모던 자바스크립트
옛날 문법이 남아있음
하위 호환성유지를 위해 덧대서 만들었다.

<div class="divider"></div>

### 자바스크립트가 할수 있는 일

자바스크립트는 웹조작, 클라이언트 서버 상호작용, 이벤트 조작, ajax
쿠키 값 가져고오거나 설정/ 사용자에게 메세지 

브라우저 쿠키 ->> 정보를 가지고 있는 값, 브라우저에 저장 
세션 ->> 파일로 서버측
캐시 ->> 서버에서 미리 받아둔 내로컬에 남아있는 정보를 이용


### 자바스크립트가 할수 없는 일 

보안 ->> 제약 많이 걸어둠 브라우저 제약
서버측 일을 할수 없었는데, nodejs
브라우저 탭 1번 탭, 2번 탭은 서로 독립적이다.
(보안)정책에 따라 할수 있는것, 할수 없는 것이 있다.
익스텐션 우회


### 자바스크립트의 강점 - 통합이 잘 되어있음

html 안에서 스크립트라는 키워드로 js, css 여러가지 사용 가능하다 (다만, 정리를 하지 않으면 지저분함)


<div class="divider"></div>



<div class="divider"></div>

### 운영체제
webos, TV 안드로이드, 타이젠

### 발전 
타입스크립트, 커피스크립트, 플로우, 다트 ..등등
슈퍼셋
타입스크립트로 작성한 것을 내부적으로는 js 변환해서 돌린다.
트렌스파일 >> 파일을 변환 시킨다.


### 공부방법
공식문서
 >> https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference
구글링  ex) django docu 최상단에 공식문서
	   ECMA docu
aka 설명서부터 읽어봐라

### 디버깅이란?
 >> 내가 의도하는대로 잘 작동하는지 확인 후 문제가 있으면 수정하는 행위

브라우저 -> 개발자도구(F12) -> 콘솔창에서 눈으로 찍어보는 것이 제일 좋음
(크롬)개발자도구 관련 유튜브 찾아봐서 공부하는 것이 제일 좋음

### 가독성
자바스크립트는 줄바꿈이 있으면
암묵적인 세미콜론으로 해석

### 명시적 암묵적 explict implict
파이썬 zen
'암묵적인것 보다는 명시적인걸 선호한다.


<div class="divider"></div>

### JavaScript 옛날 모양
```javascript
<script type="text/javascript">  
  console.log("Hello World!")
</script>
```

### JavaScript 현재 모양
```javascript
<script>  
 console.log("Hello World!")
</script>
```

<div class="divider"></div>

### JavaScript로 html 활용하기

```html
<!DOCTYPE html>

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>첫화면</title>
  <!-- 외부스크립트 가져오기 -->
  <!-- <script src="http://path/to/script.js></script> -->
  <script src=""></script>
  <!-- 경로만 정확하면 가져올 수 있다 -->
</head>
<body>
  <h1>안녕하세요</h1>
  
  <p id="myID"></p>
  <button onclick="asdf()">실행</button>
  <script>

    alert("hello world!");
    console.log("html안의 스크립트");
    function asdf() {
      return (document.getElementById("myID").innerHTML = "이너HTML")
    }
  </script>
  
</body>
</html>
```

### JavaScript로 Bootstrip

```html
<!doctype html>
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

    <!-- Bootstrap CSS -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.1.3/dist/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">

    <title>외부 js 가져오기</title>
  </head>
  <body>
    <h1>부트스트랩관련 js 가져와서 화면구성</h1>
    <script>
      alert("얼럿으로 화면에 찍기");
    </script>

    <!-- Optional JavaScript -->
    <!-- jQuery first, then Popper.js, then Bootstrap JS -->
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.14.3/dist/umd/popper.min.js" integrity="sha384-ZMP7rVo3mIykV+2+9J3UJ46jBk0WLaUAdn689aCwoqbBJiSnjAK/l8WvCWPIPm49" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.1.3/dist/js/bootstrap.min.js" integrity="sha384-ChfqqxuZUCnJSK3+MXmPNIyE6ZbWh2IMqE241rYiqJxyMiZ6OW/JmZQ5stwEULTy" crossorigin="anonymous"></script>
  </body>
</html>
```

<hr>

### 현상황
현 상황은 춘추전국시대를 끝내고 ECMA 표준으로 거의 자리잡음
옛날에는 호환성 때문에 힘든 것이 많았음
옛날에는 자바스크립트 호환성 검색을 많이했음
자동 분석해주는 사이트 존재
제이쿼리를 걷어내고, 큰 트랜드는 제이쿼리를 잘 안씀 
 >> 왜냐하면 여러가지 문제를 일으키고, 제일 큰 것은 호환성이 잘 안됨
꿀Tip) 크롬에서 잘 개발하면 웬만한 곳에서 다 호환이 잘됨

### 파이썬

```python
for  item in items:
   print()
```
### 파이썬 c 스타일
```python
for i in range(0, len(dfd)):
```

### 자바스크립트
```javascript
for (i;i<변수.length;i++){
	console.log(i);
}
```

### 자바스크립트의 주석처리
I D E 통합개발환경 (vscode)
컨트롤 슬래쉬 -> 주석처리
한줄처리 //
여러줄 /* */
부분 단축키 알트 쉬프트 A

use strict -> ?

### 변수 

선언과 동시에 값을 넣기도 하는데
var , let
let
let 변수명;
변수명 = 값;
let name = “정대호”;
alert(name);
호이스팅
 >> 맨위로 끌어올린다.