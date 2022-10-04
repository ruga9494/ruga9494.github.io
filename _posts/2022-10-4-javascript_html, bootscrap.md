---
category: javaScript
url_path: '/stuff/:id'
title: '2022.10.04 자바스크립트 html, bootsctrap 활용하기'
type: 'post'

layout: null
---

### Javascript를 활용해서 html에 적용시키기
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

### bootstrap 활용하기
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