---
title: "[jQuery] jQuery UI를 통한 토글 방향 변경"
excerpt: "jQuery UI를 사용하여 좌우로 슬라이드 토글 기능 구현"

categories:
  - jQuery
tags:
  - [Javascript, jQuery]

comments: true
toc: true
toc_sticky: true

date: 2021-07-21
last_modified_at: 2021-07-21
---

# jQuery UI를 알게 된 계기

오늘 사이드바에서 슬라이드-토글하는 탭메뉴를 하드코딩했다.

![image](https://user-images.githubusercontent.com/86935775/126513009-a0326059-a9b0-4223-a6ee-590a8aab6b8e.png)

이렇게 된 메뉴에서 탭을 누르면

![image](https://user-images.githubusercontent.com/86935775/126513101-1036140a-cdf2-4ae5-aa55-14c58af49153.png)

이렇게 탭과 내용이 나타나는 메뉴인데 열려있는 상태에서 다시 누르면 내용이 닫히게끔 구현하기 위해 jQuery에서 기본으로 제공되는 `.slideToggle()` 메서드를 사용하고자 했다.

> `.slideToggle()` 메서드는 선택한 DOM 요소가 슬라이드 애니메이션을 하며 show와 hide를 반복하는 메서드이다.

[slideToggle() 메서드 사용법](https://api.jquery.com/slidetoggle/)

<br><br>
그러나 `.slideToggle()` 메서드는 **show와 hide시에 슬라이드를 수직으로만 동작**했다.

정확히는 show 동작시 위에서 아래로 slide 하며 나타났고,

hide 시에는 아래서 위로 silide하며 사라졌다.

<br><br>

내가 원하는 좌우로 toggle하는 기능 구현을 위해서는 좌/우로 슬라이드하는 메서드가 필요했다.

<br>

검색 결과, stack overflow 사이트에서 답을 찾을 수 있었다.

![image](https://user-images.githubusercontent.com/86935775/126514768-11bef202-4185-454a-b77f-1eb6133bf7b4.png)

```javascript
$(this).toggle("slide", { direction: "right" }, 1000);
```

위처럼 코딩을 하면 좌우로 슬라이딩 할 수 있게 된다.

다만 댓글 10번과 같이 jQuery UI를 import해야한다.

<br><br>

jQuery UI import 구문은 아래와 같다.

```html
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
```

<br><br>
jQuery UI에 대해서는 다음에 더 자세히 알아보도록 하겠다.
