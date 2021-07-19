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

# Slick Slide 사용 준비

<https://kenwheeler.github.io/slick/>
