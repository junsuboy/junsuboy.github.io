---
title: "[React.js] Hook이란?"
excerpt: "React Hook의 정의와 간단한 사용 예제"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-08-02
last_modified_at: 2021-08-02
---

# React Hook이란?

![image](https://user-images.githubusercontent.com/86935775/128110715-403ac3ce-7e30-4917-ab15-a43d99ea1c77.png)

> *Hook*은 React 16.8에 새로 추가된 기능입니다. *Hook*은 class를 작성하지 않고도 state와 다른 React의 기능들을 사용할 수 있게 해줍니다.

Hook은 함수 컴포넌트에서 **React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수**입니다. **Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것**입니다.

<br><br>

## Hook을 사용하는 이유

리액트 컴포넌트는 **클래스형 컴포넌트(Class Component)**와 **함수형 컴포넌트(Functional Component)**로 나뉩니다.

기존의 개발방식은 일반적으로 함수형 컴포넌트를 주로 사용하되 state이나 Life Cycle method를 사용해야 할 때에만 클래스형 컴포넌트를 사용하는 방식이었습니다.

이유는 클래스형 컴포넌트가 함수형 컴포넌트에 비해 가지는 단점 때문입니다.

<br><br>

**1. 코드가 길고 복잡합니다.**

**constructor, this, binding** 등 지켜야 할 규칙이 많아서 코드가 복잡하고 길어집니다.

JAVA처럼 OOP(Object-oriented programming)의 테크닉을 수려하게 적용하지는 않으면서도 근본은 클래스의 모습을 띄고 있죠.

클래스 자체가 **Life Cycle method**로 인해 기본적으로 뚱뚱합니다.

<br>

**2. Logic의 재사용이 어렵습니다.**

클래스형 컴포넌트에서는 High-Order Components(HOC)로 컴포넌트 자체를 재사용 할 수는 있지만 **부분적인 DOM 관련 처리나 API사용 및 state을 다루는 등의 logic**에 있어서는 경우에 따라 같은 로직을 2개 이상의 Life Cycle method에 중복해서 넣어야하는 등 재사용에 제약이 따릅니다.

이에 반해 **hooks를 활용한 함수형 컴포넌트에서는 원하는 기능을 함수로 만든 후(hook) 필요한 곳에 훅 집어 넣어주기**만 하면 되기 때문에 로직의 재사용이 가능해집니다.

<br><br>

> Hooks

함수형 컴포넌트에 비해 가지는 이러한 단점들에도 불과하고, 그동안 클래스형 컴포넌트를 사용했던 이유는 위에서 언급했듯이 state관리와 Life cycle method의 사용때문이었습니다.

복잡하고 뚱뚱하지만

클래스의 힘을 빌려야만 React가 원활하게 작동할 수 있었던 것입니다.

그런데 hooks의 등장으로 인해 함수형 컴포넌트에서도 이러한 클래스형 컴포넌트의 작업들을 할 수 있게 되었습니다.

기존의 클래스형 컴포넌트가 가지고 있던 복잡성, 재사용성의 단점들까지 해결하면서 말입니다.

<hr><br><br>

# 📌 State Hook

버튼을 클릭하면 값이 증가하는 간단한 카운터 예시를 보겠습니다.

```javascript
import React, { useState } from "react";

function Example() {
  // "count"라는 새 상태 변수를 선언합니다
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
// 본 예제에서는 count가 state 역할을 합니다.
```

여기서 `useState`가 바로 Hook 입니다. Hook을 호출해 함수 컴포넌트(function component) 안에 state를 추가했습니다. 이 state는 컴포넌트가 다시 렌더링 되어도 그대로 유지될 것입니다. `useState`는 현재의 state 값과 이 값을 업데이트하는 함수를 쌍으로 제공합니다. 우리는 이 함수를 이벤트 핸들러나 다른 곳에서 호출할 수 있습니다. 이것은 class의 `this.setState`와 거의 유사하지만, 이전 state와 새로운 state를 합치지 않는다는 차이점이 있습니다.

`useState`는 인자로 초기 state 값을 하나 받습니다. 카운터는 0부터 시작하기 때문에 위 예시에서는 초기값으로 `0`을 넣어준 것입니다. `this.state`와는 달리 `useState` Hook의 state는 객체일 필요가 없습니다. 물론 원한다면 그렇게도 가능합니다. 이 초기값은 첫 번째 렌더링에만 딱 한번 사용됩니다.

<br><br>

# ⚡️ Effect Hook

React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 “side effects”(또는 짧게 “effects”)라고 합니다. 왜냐하면 이것은 다른 컴포넌트에 영향을 줄 수도 있고, 렌더링 과정에서는 구현할 수 없는 작업이기 때문입니다.

Effect Hook, 즉 `useEffect`는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해줍니다. React class의 `componentDidMount` 나 `componentDidUpdate`, `componentWillUnmount`와 같은 목적으로 제공되지만, 하나의 API로 통합된 것입니다.

아래 예제는 React가 DOM을 업데이트한 뒤에 문서의 타이틀을 바꾸는 컴포넌트입니다.

<br><br>

```javascript
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount, componentDidUpdate와 비슷합니다
  useEffect(() => {
    // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

<br><br>

`useEffect`를 사용하면, React는 DOM을 바꾼 뒤에 “effect” 함수를 실행할 것입니다. Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있습니다. 기본적으로 React는 첫번째 렌더링을 포함한 매 렌더링 이후에 effects를 실행합니다.

Effect를 “해제”할 필요가 있다면, 해제하는 함수를 반환해주면 됩니다. 이는 선택적입니다(optional). 예를 들어, 이 컴포넌트는 친구의 접속 상태를 구독하는 effect를 사용했고, 구독을 해지함으로써 해제해줍니다.

<br><br>

```javascript
import React, { useState, useEffect } from "react";

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

이 예시에서 컴포넌트가 unmount될 때 React는 `ChatAPI`에서 구독을 해지할 것입니다. 또한 재 렌더링이 일어나 effect를 재실행하기 전에도 마찬가지로 구독을 해지합니다. (만약 원한다면 `props.friend.id`가 바뀌지 않았을 때 재구독을 건너뛰도록 설정할 수 있습니다.)

`useState`와 마찬가지로 컴포넌트 내에서 여러 개의 effect를 사용할 수 있습니다.

<br><br>

```javascript
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

<br>
<br>

# ✌️ Hook 사용 규칙

Hook은 그냥 JavaScript 함수이지만, 두 가지 규칙을 준수해야 합니다.

- **최상위(at the top level)** 에서만 Hook을 호출해야 합니다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행할 수 없습니다.

- **React 함수 컴포넌트** 내에서만 Hook을 호출해야 합니다. 일반 JavaScript 함수에서는 Hook을 호출해서는 안 됩니다. (Hook을 호출할 수 있는 곳이 딱 한 군데 더 있습니다. 바로 직접 작성한 custom Hook 내입니다)

이 규칙들을 강제하기 위해서 [linter plugin](https://www.npmjs.com/package/eslint-plugin-react-hooks)을 제공하고 있습니다. 이 규칙들이 제약이 심하고 혼란스럽다고 처음에는 느낄 수 있습니다. 하지만 이것은 Hook이 제대로 동작하기 위해서는 필수적인 조건입니다.

<br><br><br>

[참고 링크 : React Hook Document](https://ko.reactjs.org/docs/hooks-intro.html)
