---
title: "[Javascript] Slick Slider 라이브러리 사용하기"
excerpt: "Slick Slider Library를 사용하여 다양한 슬라이드 구현해보기"

categories:
  - Javascript
tags:
  - [Javascript]

comments: true
toc: true
toc_sticky: true

date: 2021-07-19
last_modified_at: 2021-07-19
---

# 더미 이미지 무료 제공 사이트

우선 슬라이드에 사용할 이미지를 아래 링크에서 가져 올 예정이다.

<https://placeimg.com>

사용 방법:

```html
<img src="https://placeimg.com/가로크기/세로크기/카테고리" />
```

카테고리에 사용할 수 있는 주제(키워드)는 다음과 같다.
`animals`, `architecture`, `nature`, `people`, `tech`
![image](https://user-images.githubusercontent.com/86935775/126181407-949aa0ae-a78f-41a8-b565-eaca2ee5cf3b.png)

아래는 가로 300, 세로 300, 주제 animals로 불러온 더미 이미지이다.

<img src="https://placeimg.com/300/300/animals">

더미 이미지기 때문에 새로고침을 할 때 마다 다른 사진으로 변경된다.

위와 같이 원하는 사이즈의 더미 이미지를 손쉽게 불러올 수 있는 링크를 이용해 슬라이드를 작성할 예정이다.

<br><br>

# Slick Slider 라이브러리 사용 예제

Slick Slider란 반응형 웹을 지원하는 슬라이더 라이브러리다.

<https://kenwheeler.github.io/slick/>
<br><br>

## Slick Slider 라이브러리 다운받기

Slick Slider 사이트에서 라이브러리를 다운받을 수 있다. 아래 사진과 같이 **get it now**를 클릭하면

![image](https://user-images.githubusercontent.com/86935775/126184026-e95d9582-50f8-47c7-ad07-ccd9f6e082d4.png)

zip 형태의 파일로 다운받거나,
Github에서 프로젝트 전체에 접근할 수 있다.

![image](https://user-images.githubusercontent.com/86935775/126184249-5ac0aa75-1bf9-40b1-bc39-778ebc0257d4.png)

파일 구조는 다음과 같다.
![image](https://user-images.githubusercontent.com/86935775/126186031-d918c5fd-3f23-4bc3-88e3-487cdf5afdab.png)

`index.html` 파일을 열면, 심플한 사용 예제를 볼 수 있고,
실질적인 라이브러리 파일은 `slick` 폴더 내부에 있다.

![image](https://user-images.githubusercontent.com/86935775/126186402-64a89594-253d-4999-9bd5-73e3fe561ab0.png)

이 포스팅에서는 JQuery를 사용하여 예제를 작성할 것이므로,
`slick.js`, `slick.css`, `slick-theme.css` 파일을 사용할 것이다.

<br><br>

## js, css 파일 로드

아래와 같이 `head` 내에 `css`, `jQuery`, 그리고 `slick.js`를 불러온다. <br>
기본적으로 slick slider는 `jQuery` 기반으로 만들어진 라이브러리라 `jQuery`가 필요하므로 함께 CDN으로 불러온다.<br>
일반적으로 `.min.js`는 `.js` 파일에서 줄바꿈을 제거하여 경량화한 버전이다.

```html
<link rel="stylesheet" href="slick.css" />
<link rel="stylesheet" href="slick-theme.css" />
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
<script src="slick.min.js"></script>
```

이 때 조심해야 할 것이 있는데 `slick.js`는 `jQuery`를 호출한 이후에 호출되어야 한다. 그렇지 않으면 슬라이드가 정상적으로 동작하지 않는다. 처음 예제를 작성할 때 위 사항을 준수하지 않아 애를 먹었다.
![image](https://user-images.githubusercontent.com/86935775/126187880-3fd8b2aa-2533-4cb5-8bff-56ed1cbd073b.png)
<br><br>

## 동작 방식

slick slider의 기본 HTML 구성은 아래의 코드처럼 div의 형태로 구성되어 있는 html 문서를 슬라이더 형태로 변경을 해준다.

만약 div 형태가 아닌 다른 태그는 아래 써둔 slide 옵션을 조정하면 된다.

```javascript
<script>
  $(function () {
    $("#slider-div").slick({
      slide: "div", //슬라이드 되어야 할 태그 ex) div, li
      infinite: true, //무한 반복 옵션
      slidesToShow: 4, // 한 화면에 보여질 컨텐츠 개수
      slidesToScroll: 1, //스크롤 한번에 움직일 컨텐츠 개수
      speed: 100, // 다음 버튼 누르고 다음 화면 뜨는데까지 걸리는 시간(ms)
      arrows: true, // 옆으로 이동하는 화살표 표시 여부
      dots: true, // 스크롤바 아래 점으로 페이지네이션 여부
      autoplay: true, // 자동 스크롤 사용 여부
      autoplaySpeed: 10000, // 자동 스크롤 시 다음으로 넘어가는데 걸리는 시간 (ms)
      pauseOnHover: true, // 슬라이드 이동	시 마우스 호버하면 슬라이더 멈추게 설정
      vertical: false, // 세로 방향 슬라이드 옵션
      prevArrow:
        "<button type='button' class='slick-prev'>Previous</button>", // 이전 화살표 모양 설정
      nextArrow: "<button type='button' class='slick-next'>Next</button>", // 다음 화살표 모양 설정
      dotsClass: "slick-dots", //아래 나오는 페이지네이션(점) css class 지정
      draggable: true, //드래그 가능 여부

      responsive: [
        // 반응형 웹 구현 옵션
        {
          breakpoint: 960, //화면 사이즈 960px
          settings: {
            //위에 옵션이 디폴트 , 여기에 추가하면 그걸로 변경
            slidesToShow: 3,
          },
        },
        {
          breakpoint: 768, //화면 사이즈 768px
          settings: {
            //위에 옵션이 디폴트 , 여기에 추가하면 그걸로 변경
            slidesToShow: 2,
          },
        },
      ],
    });
  });
</script>
```

위의 다양한 속성들을 사용하여 슬라이드를 필요에 따라 커스텀할 수 있다.
<br><br>

## 사용 예제

Slick Slider 기본 사이트에서는 다양한 사용 예제를 제공한다.

간단하게 Fade 방식 슬라이드를 적용시켜보겠다.

![image](https://user-images.githubusercontent.com/86935775/126189853-5bda58b2-e2e4-487e-8556-0b4cbfa655b7.png)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      * {
        margin: 0 auto;
      }
    </style>
    <link rel="stylesheet" href="slick.css" />
    <link rel="stylesheet" href="slick-theme.css" />
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
    <script src="slick.min.js"></script>
  </head>
  <body>
    <div class="slider">
      <div>
        <img src="https://placeimg.com/300/300/animals" alt="" />
      </div>
      <div>
        <img src="https://placeimg.com/300/300/architecture" alt="" />
      </div>
      <div>
        <img src="https://placeimg.com/300/300/people" alt="" />
      </div>
      <div>
        <img src="https://placeimg.com/300/300/tech" alt="" />
      </div>
    </div>
    <script>
      $(document).ready(function () {
        $(".slider").slick({
          dots: true,
          infinite: true,
          speed: 500,
          fade: true,
          cssEase: "linear",
        });
      });
    </script>
  </body>
</html>
```

**실행결과**

![image](https://user-images.githubusercontent.com/86935775/126190174-521ab674-3eca-4c4c-acf2-7a56c4f67392.png)
![image](https://user-images.githubusercontent.com/86935775/126190263-8bc13b49-3e67-4f5e-8133-be5a6642aaa6.png)

위와 같이 다양한 예제를 사용하거나, 직접 슬라이드의 속성을 커스텀하여 사용하면 되겠다.

<br><br>

## 유용한 함수

**slider 제거하기**<br>
slick을 unslick 하지 않은 상태에서 다시 slick을 하면 Cannot read property 'add' of null 에러가 뜬다.

따라서 이미 만들어진 slick을 제거한 후 다시 slick을 해줘야 제대로 슬라이더가 만들어진다.

```javascript
// slick 파괴
$("#slider-div").slick("unslick");
```

**slider에 새로운 아이템 추가하기**<br>
이미 slick이 적용이 되어 있는 상태에서 슬라이더를 동적으로 추가하고 싶다면 다음과 같은 옵션을 사용하면 된다.

```javascript
$("#slider-div").slick("slickAdd", "<div>새로운 아이템</div>");
```

**slider에 있는 아이템 삭제하기**<br>
인자값으로 여러가지를 줄 수 있다.

```javascript
$("#slider-div").slick("slickRemove", 0); //특정 인덱스 번호에 있는 slider 삭제

$("#slider-div").slick("slickRemove", false); //false이면 맨 마지막 슬라이더 삭제
$("#slider-div").slick("slickRemove", true); // true이면 맨 앞 슬라이더 삭제
```

**현재 보여지는 슬라이더가 몇번째 슬라이더인지 확인하기**

```javascript
$("#slider-div").slick("slickCurrentSlide"); // 가장 첫번째에 있는 슬라이드는 0번이다.
```

**자동 슬라이드 넘기기 정지 / 시작**

```javascript
$("#slider-div").slick("slickPause"); // 정지
$("#slider-div").slick("slickPlay"); // 시작
```

**원하는 슬라이드로 이동**

```javascript
$("#slider-div").slick("goTo", 1); // slick('goTo', index ) index는 0부터 시작이다.
```
