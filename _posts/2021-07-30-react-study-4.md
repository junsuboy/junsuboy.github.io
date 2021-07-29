---
title: "[React.js] state란"
excerpt: "state를 사용하는 이유, class Component를 사용하는 이유, state를 변화시키는 방법"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-07-30
last_modified_at: 2021-07-30
---

# state란?

**state**는 동적(dynamic) 데이터와 함께 작업할 때 만들어진다. 변하는 데이터, 존재하지 않는 데이터
생겨나고 사라지는 또는 변경된 데이터, 하나인 데이터 그리고 두개가 되고 또 0이 되는 그런 종류의 데이터
- state는 object이다.
- Component의 data를 넣을 공간이 있고, 이 data는 동적이다.

<br><br>

# class Component란?

class Component
- **render method** 사용 가능
- class이지만 React Component로부터 확장되고 screen에 표시된다. 이는 render method 안에 포함되어야 한다.
- React는 자동적으로 모든 class Component의 render method를 실행하고자 한다.
- class Component를 사용하는 이유는 일반적으로 state 때문이다.

선언 방식

```javascript
class App extends React.Component {
  state = {
    count: 0,
  };

  add = () => {
    this.setState(current => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState({ count: this.state.count - 1 });
  };

  render() {
    return (
      <div>
        <h1>The number is: {this.state.count}</h1>
        <button onClick={this.add}>Plus</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
}
```

`extends React.Component`는 React Class의 자식 클래스임을 의미한다.

그로 하여금 React 클래스에 사용된 여러 메서드를 사용할 수 있게 된다.

<br><br>

# state를 변경시키는 방법

state를 변경하기 위해서는 `setState()` 메서드를 사용해야 함.

- `setState()`를 사용하지 않으면 새 state와 함께 render function이 호출되지 않음

- `setState()`를 호출할 때 마다 React는 새로운 state와 함께 render function을 호출함

```javascript
import React from "react";
import PropTypes from "prop-types";

class App extends React.Component {
  state = {
    count: 0,
  };

  add = () => {
    this.setState(current => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState({ count: this.state.count - 1 });
  };

  render() {
    return (
      <div>
        <h1>The number is: {this.state.count}</h1>
        <button onClick={this.add}>Plus</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
```

위와 같이 state를 선언하고
```javascript
state = {
    count: 0,
  };
```

count를 변화시키는 함수를 선언한다. 이 때 사용하는 함수는 javascript이다.

minus 함수에 사용되는 문법은 사용 가능하지만 권장되지 않는다.
add 함수에 사용되는 것과 같이 state를 직접 호출하지 않는 것이 외부 환경에 영향을 받지 않으므로 바람직하다.

```javascript
  add = () => {
    this.setState(current => ({ count: current.count + 1 }));
  };
  minus = () => {
    this.setState({ count: this.state.count - 1 });
  };
```

render method에서 `this.state.count`로 `<h1>` 태그 내에 `count`를 불러오고, 각 Plus와 Minus 버튼에 `onClick` props로 add 함수와 minus 함수를 이벤트 추가한다.

```javascript
  render() {
    return (
      <div>
        <h1>The number is: {this.state.count}</h1>
        <button onClick={this.add}>Plus</button>
        <button onClick={this.minus}>Minus</button>
      </div>
    );
  }
```

<br><br>

## 실행결과

![image](https://user-images.githubusercontent.com/86935775/127474067-c1c7916c-21af-46f1-addf-051984d543e3.png)

![image](https://user-images.githubusercontent.com/86935775/127474172-a9fd826e-15cc-4ff9-873d-c172af8d663b.png)

위와 같이 Plus 버튼을 누르면 count가 증가하여 실시간으로 화면에 rendering 되는 것을 확인할 수 있다.

이 때, 개발자 도구에서 Elements를 확인하면 오로지 count 부분만 변경되는 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/86935775/127474415-3cf7ca6a-994a-4a62-8fd7-e1e9d7e997b2.png)

이것은 React 프레임워크가 **Virtual DOM을 사용하기 때문**이며 React의 강점이다.