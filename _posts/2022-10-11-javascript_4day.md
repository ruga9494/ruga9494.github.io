---
title: Javascript 4일차
updated: 2022-10-07 09:01
---

### 3의 배수 찾기

```javascript
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
    <script>
      var i;
      var userNumber = parseInt(prompt("몇 까지 3의 배수를 찾을까요?", "100"));
      var count = 0;

      if (userNumber !== null) {
        document.write(
          '<div class="container"><table class="table"><thead><tr><th scope="col">연번</th><th scope="col">3의 배수</th></tr></thead><tbody>'
        );
        for (i = 0; i < userNumber; i++) {
          if (i % 3 === 0) {
            count++;
            // document.write(i);
            // document.write("<br>");
            document.write(`<tr><th scope="row">${i}</th><td>${i}</td></tr>`);
          }
        }
        // document.write("<p>"+ userNumber + "까지 3의 배수의 갯수 : " + count + "</p>");
        document.write("</tbody></table><p></p></div>");
        document.write(
          `<p>${userNumber}까지 3의 배수의 갯수 : ${count} 입니다</p>`
        );
      }
    </script>
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-OERcA2EqjJCMA+/3y+gxIOqMEjwtxJY7qPCqsdltbNJuaOe923+mo//f6V8Qbsw3"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```

<div class="divider"></div>

### 배열 누적합 구하기

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>1에서 5까지 더하기</title>
	<style>
		body {
			font-size:1.5em;
			line-height:2;
			text-align:center;
		}
	</style>
</head>
<body>
	<script>
		var i;
		var sum = 0;

    const 배열 = [];
		for(i = 1; i < 1001; i++) {
      // sum += i;						
			배열.push(i);
		}
    
    console.log(배열);

    const 누적합 = 배열.map(function(){
      return this.누적합 += i
    }, {누적합:0});
    // map
    console.log(누적합);
   
		document.write("1부터 5까지 더하면 " + sum);
	</script>
</body>
</html>


    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-OERcA2EqjJCMA+/3y+gxIOqMEjwtxJY7qPCqsdltbNJuaOe923+mo//f6V8Qbsw3"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```
<div class="divider"></div>

### or 연습

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>조건문</title>
</head>
<body>
  <script>
    var numberOne = prompt("50미만의 숫자를 입력하세요.");
    var numberTwo = prompt("50미만의 숫자를 입력하세요.");

    if (numberOne < 10 || numberTwo < 10) 
      alert("두 개의 숫자 중 최소한 하나는 10 미만이군요.");
    else 
      alert("두 개의 숫자 중 10 미만인 수는 없습니다.");
  </script>
</body>
</html>
```

<div class="divider"></div>

### if 연습

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>조건문</title>
</head>
<body>
    <script>
      var userNumber = prompt("숫자를 입력하세요.");

      if (userNumber !== null) 
        (userNumber % 3 === 0) ? alert("3의 배수입니다.") : alert("3의 배수가 아닙니다.");
      else 
        alert("입력이 취소됐습니다.");      
    </script>
</body>
</html>
```

<div class="divider"></div>

### 구구단

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>구구단 - for문</title>
	<link rel="stylesheet" href="css/gugudan-table.css">
<body>
	<h1>구구단</h1>
	<script>
		var i, j;

		for (i = 1; i <= 9; i++) {
			document.write("<table>");
			document.write("<tr><th>" + i + "단</th></tr>");
			for (j = 1; j <= 9; j++) {
				document.write("<tr><td>" + i +" X " + j + " = " + i*j + "</td></tr>");
			}
			document.write("</table>");
		}
	</script>
</body>
</html>
```
<div class="divider"></div>

### 팩토리얼

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>팩토리얼 계산하기</title>
	<style>
		body {
			padding-top:20px;
			text-align:center;
		}
	</style>
</head>
<body>
	<h1>while문을 사용한 팩토리얼 계산</h1>

	<script>
			var n = prompt("숫자를 입력하세요.","10");
			var msg = "";

			if (n !== null) {  // '취소' 버튼을 누르지 않았는지 체크
				var nFact = 1;  // 결과 값
				var i = 1;  // 카운터
				
				while(i <= n) {
					nFact *= i;
					i++;
				}
				msg = n + "! = " + nFact;  // 결과 값을 표시할 문자열 
			}
			else
				msg = "값을 입력하지 않았습니다.";

			document.write(msg);  // 결과 표시
	</script>
</body>
</html>
```
<div class="divider"></div>

### 짝수끼리 더하기

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>짝수 더하기</title>
	<style>
		body {
			padding-top:20px;
			text-align:center;
		}
	</style>
</head>
<body>
	<h1>짝수끼리 더하기</h1>
	<script>
		var i;
		var n = 10;
		var sum = 0;

		for (i = 1; i <= n; i++) {
			if (i % 2 === 1)
				continue
			sum += i;

		document.write(i + " ------ " + sum + "<br>");
		}
	</script>
</body>
</html>
```
<div class="divider"></div>

### 사용자에게 입력받아 홀수끼리 더하기

```javascript
<!DOCTYPE html>
<html lang="ko">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>짝수 더하기</title>
	<style>
		body {
			padding-top:20px;
			text-align:center;
		}
	</style>
</head>
<body>
	<h1>홀수끼리 더하기</h1>
	<script>
    // 사용자에게 입력받기
		var i;
		var n = prompt("몇까지 실행할까요?", 100);
		var sum = 0;

    // 0부터 시작하기
		for (i = 1; i <= n; i++) {
			if (i % 2 === 0)
      // 값이 0 이면 홀수만 출력, 값이 1이면 짝수만 출력
				continue
        // 컨티뉴 브레이크
			sum += i;

		document.write(i + " ------ " + sum + "<br>");
		}
	</script>
</body>
</html>
```