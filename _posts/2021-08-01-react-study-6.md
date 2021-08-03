---
title: "[React.js] React Router DOM"
excerpt: "React Router DOM을 활용하여 페이지를 이동하는 방법"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-08-01
last_modified_at: 2021-08-01
---

# React Router

[![image](https://user-images.githubusercontent.com/86935775/127979398-8f7bc91b-54e6-428e-b0b9-a0115ed05e80.png)](https://reactrouter.com/web/guides/quick-start)

리액트의 _SPA(single page application)_ 구현에 가장 많이 쓰이는 라우터 중 하나

> SPA : 화면의 header, footer, sidebar 등 다시 로드해도 변함이 없는 부분들은 그대로 유지한 채 변경되는 부분의 데이터만 가져와서 수정하는 웹사이트.
>
> 리액트로 SPA를 구현한다는 것은 곧 해당 요청에 맞는 컴포넌트만 라우팅하여 부분적으로 렌더링한다는 것을 의미한다.

<br>

이 때 요청에 맞는 컴포넌트를 매칭시키기 위해 react-router-dom을 사용

<br><br>

# react-router, react-router-dom, react-router-native

**react-router-dom** : 웹에서 쓰이는 컴포넌트를 포함한다.

**react-router-native** : react-native를 활용한 앱개발에 쓰이는 컴포넌트를 포함한다.

**react-router**는 이 둘을 합친 패키지이다.

웹개발을 위해서는 react-router-dom만 설치하면 된다.

<br><br>

# React Router DOM 사용법

## 설치

```javascript
$ npm install react-router-dom
```

<br>

## import

```javascript
import { BrowserRouter, Route, Switch, Link } from "react-router-dom";
```

<br>

## Router의 종류, 기능

**`<BrowserRouter>`**

react-router-dom의 라우터는 **`<BrowserRouter>`** 와 **`<HashRouter>`** 두가지가 있다.
**`<BrowserRouter>`** 는 HTML5의 history API를 활용하여 UI를 업데이트하고 **`<HashRouter>`** 는 URL의 hash를 활용한 라우터입니다. 정적인(static)페이지에 적합하다.

<br>

보통 request와 response로 이루어지는 동적인 페이지를 제작하므로 **`<BrowserRouter>`** 가 보편적으로 쓰이므로 이 글에서도 **`<BrowserRouter>`** 를 사용하겠다.

<br><br>

**`<Route>`**

요청받은 pathname에 해당하는 컴포넌트를 렌더링한다.

<br><br>

**`<Switch>`**

path의 충돌이 일어나지 않게 **`<Route>`** 들을 관리한다.

**`<Switch>`** 내부에 **`<Route>`** 들을 넣으면 요청에 의해 매칭되는 **`<Route>`** 들이 다수 있을 때에 제일 처음 매칭되는 **`<Route>`** 만 선별하여 실행하기 때문에 충돌 오류를 방지해주며, **`<Route>`** 간에 이동 시 발생할 수 있는 충돌도 막아준다.

path와 매칭되는 **`<Route>`** 가 없을 때에 맨 밑에 default **`<Route>`** 의 실행이 보장된다. (path 속성을 명시하지 않은 **`<Route>`** )

<br><br>

**`<Link>`**

링크를 생성합니다.

<br><br>

<hr>

## 사용예제

1. **`<BrowserRouter>`** 를 불러온 후 **`<Link>`** 를 추가한다.

```javascript
// ... 생략
function App() {
  return (
    <div className="App">
      <h1>App</h1>
      <BrowserRouter>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/beauty">Beauty</Link>
          </li>
          <li>
            <Link to="/game">Game</Link>
          </li>
        </ul>
      </BrowserRouter>
    </div>
  );
}
// 생략 ...
```

위 예제에서 `a`, `href`를 사용하지 않은 이유는 `a`, `href`는 `HTML` 태그로서 페이지 전체를 새로고침하기 때문이다.

<br><br>

2. **`<Switch>`** 와 그 안에 **`<Route>`** 3개를 추가한다.

```javascript
// ... 생략
function App() {
  return (
    <div className="App">
      <h1>App</h1>
      <BrowserRouter>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/beauty">Beauty</Link>
          </li>
          <li>
            <Link to="/game">Game</Link>
          </li>
        </ul>
        <Switch>
          <Route path="/"></Route>
          <Route path="/beauty"></Route>
          <Route path="/game"></Route>
        </Switch>
      </BrowserRouter>
    </div>
  );
}

// 생략 ...
```

**`<Link>`** 를 통해 생성된 요청을 **`<Route>`** 가 받게 됐다.

**`<Link>`** 의 to 속성과 동일한 path를 가지고 있는 **`<Route>`** 가 매칭된다.

<br><br>

3. 렌더링할 컴포넌트를 생성하고 **`<Route>`** 의 component속성에 전달한다.

```javascript
import React from "react";
import { BrowserRouter, Route, Switch, Link } from "react-router-dom";

function App() {
  return (
    <div className="App">
      <h1>App</h1>
      <BrowserRouter>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/beauty">Beauty</Link>
          </li>
          <li>
            <Link to="/game">Game</Link>
          </li>
        </ul>
        <Switch>
          <Route path="/" component={Home}></Route>
          <Route path="/beauty" component={Beauty}></Route>
          <Route path="/game" component={Game}></Route>
        </Switch>
      </BrowserRouter>
    </div>
  );
}

function Home() {
  return <div>Home component</div>;
}

function Beauty() {
  return <div>Beauty component</div>;
}

function Game() {
  return <div>Game component</div>;
}

export default App;
```

Home, Beauty, Game 컴포넌트를 생성하고 component 속성으로 전달했다.

이제 매칭된 **`<Route>`** 의 컴포넌트가 렌더링된다.

그러나 아래와 같이 오류가 발생한다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbCpdGh%2FbtqxLVsjutz%2F7ueEL16B0S9iyOAm5uZ2qk%2Fimg.gif){: .align-center}

클릭할 때마다 각각 / , /beauty, /game에 해당되는 요청을 잘 받고있지만

매칭되는 **`<Route>`** 의 component를 렌더링하지 않고 항상 Home 컴포넌트만 렌더링하고 있다.

그 이유는 **`<Route>`** 의 순서 때문이다.

```javascript
<Route path="/" component={Home}></Route>
<Route path="/beauty" component={Beauty}></Route>
<Route path="/game" component={Game}></Route>
```

**`<Switch>`** 는 매칭되는 제일 첫번째의 **`<Route>`** 를 선별하는데, 첫번째 **`<Route>`** 의 path에 전달한 "/"는 모든 요청에 매칭된다. 따라서 항상 Home 컴포넌트만 렌더링 된 것이다.

이 때는 **`<Route>`** 에 exact 속성을 추가하면 된다.

exact 속성을 추가하면 pathname과 정확히 일치하는 때에만 해당 **`<Route>`** 를 매칭시킨다.

첫번째 **`<Route>`** 에 exact 속성을 추가한다.

```javascript
<Route path="/" exact component={Home}></Route>
<Route path="/beauty" component={Beauty}></Route>
<Route path="/game" component={Game}></Route>
```

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPoHxf%2FbtqxJxsG9G9%2FCBraeGBAxpYKNtcvFY0ik1%2Fimg.gif){: .align-center}

요청에 맞게 해당되는 컴포넌트가 렌더링 되었다.
