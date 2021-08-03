---
title: "[React.js] React와 axios"
excerpt: "React에서 axios를 사용하는 방법"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-07-31
last_modified_at: 2021-07-31
---

# axios란?

![image](https://user-images.githubusercontent.com/86935775/127974133-3ff20a8c-0c4c-43fd-9321-2513252a5ae2.png)

Axios는 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신 라이브러리이다.
(백엔드와 프론트엔드와 통신을 쉽게하기 위해 AJAX도 더불어 사용하기도 한다.)

<br><br>

## axios 특징

- 운영 환경에 따라 브라우저의 XMLHttpRequest 객체 또는 Node.js의 HTTP API 사용
- Promise(ES6) API 사용
- 요청과 응답 데이터의 변형
- HTTP 요청 취소 및 요청과 응답을 JSON 형태로 자동 변경

<br><br>

## axios vs Fetch API

우리는 일반적으로 자바스크립트에서 API를 연동하기 위해서 보통 `Fetch API`를 사용하곤 했다.
리액트도 자바스크립트 built-in 라이브러리중 하나인 `Fetch API`라는 훌륭한 API 연동 모듈을 사용한다.
하지만 `Fetch API`는 자바스크립트의 built-in 라이브러리라는 특성 때문인지 많은 사람들이 리액트에서 `axios`를 사용하는 것을 선호한다.

<br><br>
<br><br>

# axios 사용법

## axios download

```javascript
// 터미널에서
yarn add axios // yarn을 사용할 경우

npm i axios // npm을 사용할 경우

// React Component 상위에 import
import axios from 'axios'
```

<br><br>

## HTTP Methods

**클라이언트가 웹서버에게 사용자 요청의 목적/종류를 알리는 수단**

1. **GET**
   > GET : 입력한 url에 존재하는 자원에 요청을 한다.

**문법**

```javascript
axios.get(url, [, config]);
```

> **GET은 서버에서 어떤 데이터를 가져와서 보여준다거나 하는 용도이다.**
>
> 주소에 있는 쿼리스트링을 활용해서 정보를 전달하는 것이지 GET메서드는 값이나 상태등을 바꿀 수 없다.

**예제 코드**

```javascript
//가상으로 보여주는 코드와 response 형태
import axios from "axios";

axios
  .get("https://localgost:3000/john/user")
  .then((Response) => {
    console.log(Response.data);
  })
  .catch((Error) => {
    console.log(Error);
  });
```

```javascript
[
  { id: 1, pw: "1234", name: "john" },
  { id: 2, pw: "1234", name: "sam" },
  { id: 3, pw: "1234", name: "peter" },
];
```

응답은 json 형태로 넘어온다.

<br><br>

2. **POST**
   > POST : 새로운 리소스를 생성(create)할 때 사용한다.

**문법**

```javascript
axios.post(
  "url주소",
  {
    data객체,
  },
  [, config]
);
```

> POST 메서드의 두 번째 인자는 본문으로 보낼 데이터를 설정한 객체 리터럴을 전달한다.
> **로그인, 회원가입 등 사용자가 생성한 파일을 서버에다가 업로드할때 사용한다.**
>
> Post를 사용하면 주소창에 쿼리스트링이 남지 않기때문에 GET보다 안전하다.

**예제 코드**

```javascript
axios
  .post(
    "url",
    {
      contact: "Sewon",
      email: "sewon@gmail.com",
    },
    {
      headers: {
        "Content-type": "application/json",
        Accept: "application/json",
      },
    }
  )
  .then((response) => {
    console.log(response.data);
  })
  .catch((response) => {
    console.log("Error!");
  });
```

<br><br>

3. **Delete**
   > REST 기반 API 프로그램에서 데이터베이스에 저장되어 있는 내용을 삭제하는 목적으로 사용한다.

**문법**

```javascript
axios.delete(url, [, config]);
```

> **Delete 메서드는 HTML Form 태그에서 기본적으로 지원하는 HTTP 메서드가 아니다.**
>
> Delete 메서드는 서버에 있는 데이터베이스의 내용을 삭제하는 것을 주 목적으로 하기에 두 번째 인자를 아예 전달하지 않는다.

**예제 코드**

```javascript
axios.delete("/thisisExample/list/30").then(function(response){
    console.log(response);
      }).catch(function(ex){
      throw new Error(ex)
}
```

<br><br>

4. **PUT**
   > REST 기반 API 프로그램에서 데이터베이스에 저장되어 있는 내용을 갱신하는 목적으로 사용된다.

**문법**

```javascript
axios.put(url[, data[, config]])
```

> **PUT메서드는 HTML Form 태그에서 기본적으로 지원하는 HTTP 메서드가 아니다.**
>
> PUT메서드는 서버에 있는 데이터베이스의 내용을 변경하는 것을 주 목적으로 하고 있다.

<br><br>

[상세 링크 참조 - Axios 러닝 가이드](https://xn--xy1bk56a.run/axios/guide/usage.html#get-%EC%9A%94%EC%B2%AD)
