---
title: "[Javascript] Javascript 개요"
excerpt: "Javascript 1일차 학습 내용 정리"

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

# 자바스크립트로 할 수 있는 것들

- 모바일 애플리케이션 개발
  - 페이스북의 리액트 네이티브(React Native) : 자바스크립트만으로 모든 운영체제에서 빠르게 작동하는 네이티브 애플리케이션 작성 가능
  - 안드로이드폰은 자바/코틀린(Kotlin), 아이폰은 스위프트(Swift) 프로그래밍 언어로 개발
- 데스크톱 애플리케이션 개발
  - NW.js(‘노드웹킷 제이에스’)
  - 깃허브(GitHub)에서 자바스크립트 개발 전용 텍스트 에디터인 아톰(Atom) 배포: 일렉트론
  - 일렉트론으로 개발된 애플리케이션: 마이크로소프트의 비주얼 스튜디오 코드(Visual Studio Code), 디스코드 (Discord) 클라이언트, 깃허브 데스크톱 클라이언트, 워드프레스(Wordpress) 데스크톱 클라이언트, 몽고디비 (MongoDB), 데이터 관리 도구 컴파스(Compass) 등
- 데이터베이스 관리
  - MongoDB: 데이터베이스 관리에 자바스크립트를 활용하는 대표적인 NoSQL 데이터베이스

<br><br>

# 사용 방법

Javascript 실행 방법에는 여러가지가 있다.

## Chrome - Console 기능 사용

1. Chrome Browser - F12 - Console 칸에서 명령어 입력

![image](https://user-images.githubusercontent.com/86935775/125216661-d1d40800-e2f9-11eb-8c85-33ff741fd66a.png)

## VSCode 사용

1. Visual Studio Code의 HTML 파일의 \<script> 태그 내에서 Javascript 코드 작성 후 HTML 실행

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script>
      alert("Hello World!");
    </script>
  </head>
  <body></body>
</html>
```

2. html 파일 실행 시 아래와 같이 alert로 **Hello World!** 가 출력됨을 알 수 있다.
   ![image](https://user-images.githubusercontent.com/86935775/125216775-2aa3a080-e2fa-11eb-96fc-7ab038c0ef32.png)

3. 오류 발생시 Chrome - Console에서 오류 문구 확인 가능

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script>
      alrt("Hello World!"); // 오류 : alrt라는 없는 함수로 변경
    </script>
  </head>
  <body></body>
</html>
```

![image](https://user-images.githubusercontent.com/86935775/125216822-473fd880-e2fa-11eb-86c4-46fc24e1e4ea.png)

- 템플릿 문자열은 백틱(‵) 기호로 감싸 만듦
  - 문자열 내부에 ‵${...}‵ 기호를 사용하여 표현식을 넣으면 표현식이 문자열 안에서 계산됨

![image](https://user-images.githubusercontent.com/86935775/125219770-65a8d280-e300-11eb-9479-add0b0488dd2.png)

<br><br>

### **document.write**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <script>
      let list = "";

      // 연산자를 사용합니다.
      list += "<ul>";
      list += " <li>Hello</li>";
      list += " <li>JavaScript..!</li>";
      list += "</ul>";
      // 문서에 출력합니다.
      document.write(list);
    </script>
  </head>
  <body></body>
</html>
```

![image](https://user-images.githubusercontent.com/86935775/125224797-32b70c80-e309-11eb-9aa1-2f5d44361059.png)

### **prompt("문구","placehold값")**

```html
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <script>
      // 상수를 선언합니다.
      const input = prompt("안녕하세요!!", "_default");

      // 출력합니다.
      alert(input);
    </script>
  </head>
  <body></body>
</html>
```

![image](https://user-images.githubusercontent.com/86935775/125225930-0f8d5c80-e30b-11eb-929b-8292bb61963a.png)
![image](https://user-images.githubusercontent.com/86935775/125225976-26cc4a00-e30b-11eb-9bec-80eb150b02b7.png)
![image](https://user-images.githubusercontent.com/86935775/125226021-3cda0a80-e30b-11eb-9b8b-b12162cf4e8b.png)
