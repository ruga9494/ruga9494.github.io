---
title: Javascript
updated: 2022-10-04 17:42
---

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
