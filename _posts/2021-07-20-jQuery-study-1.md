---
title: "[jQuery] jQuery 사용법"
excerpt: "jQuery 기본 구문, 선택자, 함수, 메서드 등"

categories:
  - jQuery
tags:
  - [Javascript, jQuery]

comments: true
toc: true
toc_sticky: true

date: 2021-07-20
last_modified_at: 2021-07-20
---

# jQuery란?

![image](https://user-images.githubusercontent.com/86935775/126324409-5d7e5d55-ca4f-4c79-b113-99e4500410e7.png)

**제이쿼리 라이브러리(jQuery Library)란**

- 제이쿼리는 일반 자바스크립트에서 볼 수 없는 다양한 애니메이션 효과의 구현을 위한 기능적인 함수들이 많이 추가되어 있다. 이런 함수를 그대로 불러와 사용할 수 있도록 구성된 기능적인 함수나 작은 프로그램들의 집합을 라이브러리라 한다.
- 자바스크립트 문법을 알지 못해도 간단하고 효율적인 제이쿼리 문법만으로 자바스크립트의 기능을 구현할 수 있도록 만든 자바스크립트 집합체(Javascript Library)

# jQuery 링크 방식

**다운로드 방식**

1. [제이쿼리 오피셜 웹사이트](https://www.jquery.com)
2. Download
3. Download the Compressed, production jQuery 3.6.0 클릭 후 js 파일 다운로드
4. 다운로드 JS 파일(`jquery-3.6.0.min.js`) HTML 파일에 링크하기

```html
<head>
  <meta charset="utf-8" />
  <title>제이쿼리 링크하기</title>
  <script src="jquery-3.6.0.min.js"></script>
</head>
```

<br>

**CDN 호스트 링크 방식**

1. [제이쿼리 CDN 웹사이트](https://code.jquery.com)
2. jQuery 3.x → minified 클릭
3. 제이쿼리 CDN 링크 복사 (https://code.jquery.com/jquery-3.6.0.min.js)
4. 복사된 CDN 주소를 HTML 파일에 링크하기

```html
<head>
  <meta charset="utf-8" />
  <title>제이쿼리 링크하기</title>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
```

<br><br>

# jQuery 기본 실행구문

```javascript
<script>$(document).ready(function(){실행구문});</script>

// or

// <script>
//   $(function(){
//     실행구문
//   });
// </script>

// these means..

// $('선택자').함수(function(){
//   ex)$('선택자').메서드(); // 실행구문
// })
```

- <span style="color:red">제이쿼리를 HTML 문서 내부에 적을 경우 </span><br>
  `</body>` 마감 태그 바로 위에서 작성하며 `<script>..</script>` 안에 작성한다.

- <span style="color:red">제이쿼리 파일을 링크형태로 사용할 경우 </span><br>
  `<head>..</head>` 사이에 넣어도 되고, `</body>` 마감 태그 바로 위에 넣어도 된다.
  <br><br>

# 선택자, 함수, 메서드

**선택자 종류**

- CSS 클래스 선택자
- CSS ID 선택자
- CSS 태그 선택자
- `this`
  <br>

**필수 함수 종류**

- `click`
- `mouseenter`
- `mouseleave`
  <br>

**필수 메서드 종류**

- `slideDown()`
- `slideUp()`
- `stop()`
- `show()`
- `hide()`
- `fadeIn()`
- `fadeOut()`
- `addClass()`
- `removeClass()`
- `children()`
- `siblings()`
  <br><br>

# 사용 예시

간단하게 `div` 태그를 보이고, 숨기고, 토글하는 예제이다.

**HTML**

```html
<button id="hide-btn">숨기기</button>
<button id="show-btn">보이기</button>
<button id="toggle-btn">토글</button>
<div>디 비 전</div>
```

<br>

**javascript**

```javascript
$("#hide-btn").click(function () {
  $("div").hide(); // 디비전 숨기기
});
$("#show-btn").click(function () {
  $("div").show(); // 디비전 보이기
});
$("#toggle-btn").click(function () {
  $("div").toggle(); // 디비전 토글하기
});
```

<br><br>

**실행결과**

1. 초기화면

![image](https://user-images.githubusercontent.com/86935775/126338050-4edc3039-5b16-427d-93ad-10447cc394d9.png)

2. 숨기기

![image](https://user-images.githubusercontent.com/86935775/126338201-85195a01-0f7d-4266-a443-64e99da32ce4.png)

3. 보이기

![image](https://user-images.githubusercontent.com/86935775/126338050-4edc3039-5b16-427d-93ad-10447cc394d9.png)

4. 토글

![image](https://user-images.githubusercontent.com/86935775/126338050-4edc3039-5b16-427d-93ad-10447cc394d9.png)

![image](https://user-images.githubusercontent.com/86935775/126338201-85195a01-0f7d-4266-a443-64e99da32ce4.png)

...
