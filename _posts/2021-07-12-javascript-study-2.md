---
title: "[Javascript] Countdown, 입력 값 읽어오기, 응용"
excerpt: "구글링해서 만든 간단한 코드"

categories:
  - Javascript
tags:
  - [Javascript]

comments: true
toc: true
toc_sticky: true

date: 2021-07-12
last_modified_at: 2021-07-12
---

# 예제1. CountDown

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div id="div1"></div>

    <script>
      var count = 9;
      var target = document.getElementsByTagName("div")[0];

      function countDown() {
        if (count != 0) {
          div1.innerHTML = count;
          count -= 1;
        } else {
          div1.innerHTML = "폭발";
          target.style.transition = "1s";
          target.style.transform = "scale(2.5)";
          target.style.backgroundColor = "red";
          clearInterval(repeat);
        }
      }
      div1.innerHTML = count + 1;
      var repeat = setInterval(countDown, 1000);
    </script>
  </body>
</html>
```

# 예제2. Input-Return

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <input id="name" onkeyup="printName()" />
    <div id="result"></div>

    <script>
      function printName() {
        const name = document.getElementById("name").value;
        document.getElementById("result").innerText = name;
      }
    </script>
  </body>
</html>
```

# 예제3. Countdown_cancel

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <p>정답인 3을 입력하면 폭탄이 해제됩니다.</p>
    <input id="name" onkeyup="compareAnswer()" />
    <div id="div1"></div>

    <script>
      var count = 9;
      var target = document.getElementsByTagName("div")[0];
      var answer = document.getElementById("name").value;

      function compareAnswer() {
        const name = document.getElementById("name").value;
        if (name == "3") {
          count = -1;
        }
      }

      function countDown() {
        if (count > 0) {
          div1.innerHTML = count;
          count -= 1;
        } else if (count == -1) {
          div1.innerHTML = "해제";
          target.style.transition = "1s";
          target.style.transform = "scale(2.5)";
          target.style.backgroundColor = "blue";
          clearInterval(repeat);
        } else {
          div1.innerHTML = "폭발";
          target.style.transition = "1s";
          target.style.transform = "scale(2.5)";
          target.style.backgroundColor = "red";
          clearInterval(repeat);
        }
      }

      div1.innerHTML = count + 1;

      var repeat = setInterval(countDown, 1000);
    </script>
  </body>
</html>
```
