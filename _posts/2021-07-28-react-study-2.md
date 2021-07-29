---
title: "[React.js] map, object, return"
excerpt: "map 메서드 동작 원리와 React에서 Object를 생성하고 활용하는 법"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-07-28
last_modified_at: 2021-07-28
---

# map 메서드

![post1](https://user-images.githubusercontent.com/86935775/127449145-d1745e5d-c4e4-4f8a-81c3-962a0422658b.PNG)

**map은 function을 취해서 그 function을 array의 각 item에 적용함
그리고 각 연산의 결과로 array를 만들고, 각 연산의 result는 항상 0임**

=> [0, 0, 0, 0] array가 됨 (return 0을 item마다 해줬기 때문)

![post2](https://user-images.githubusercontent.com/86935775/127449276-5d6d6b88-b5a9-4673-9341-1e067b45bf85.PNG)

`return current`(argument)를 했을 경우, 원래 배열값이 그대로 적용됨

![post3](https://user-images.githubusercontent.com/86935775/127449443-c32629d9-db1c-45bf-9423-31857df95159.PNG)

위와 같이 무언가 연산을 해서 return할 수도 있음

<br><br>

# props 2개를 활용한 map 예제

```javascript
import React from "react";
// react 사용시 필수 선언

function Food({ name, picture }) {
// name과 picture은 아래 object에서 정의한 props
  return (
    <div>
      <h2>I like {name}</h2> // name props 사용
      <img src={picture}> /> // image props 사용
    </div>
  );
}

function App() {
  return (
    <div className="App">
      {foodILike.map((dish) => (
        <Food name={dish.name} picture={dish.image} />
      ))}
    </div>
  );
} // function Food에 dish(foodILike의 Element)를 map으로 1번씩 props인 name과 picture를 전달함. 여기서 <Food name={dish.name} picture={dish.image} /> 이 없다면, name과 picture를 argument로 사용하는 function Food는 제대로 동작하지 않음

const foodILike = [
  // foodILike Object 선언
  {
    name: "kimchi",
    image:
      "https://kstory365.files.wordpress.com/2015/01/kimchi-01-cabbage.jpg",
  },
  {
    name: "ramen",
    image:
      "https://i.huffpost.com/gen/1410937/thumbs/o-RAMEN-facebook.jpg#Ramen%202000x1000",
  },
  {
    name: "samgyeopsal",
    image:
      "https://www.gildedgingerbread.com/wp-content/uploads/2017/08/Samgyeopsal-1.jpg",
  },
  {
    name: "kimbap",
    image:
      "https://www.maangchi.com/wp-content/uploads/2007/08/gimbap_plate.jpg",
  },
  {
    name: "bibimbap",
    image:
      "https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Dolsot-bibimbap.jpg/1200px-Dolsot-bibimbap.jpg",
  },
];

export default App;
```

<br><br>

# 실행결과

![image](https://user-images.githubusercontent.com/86935775/127450418-2b1849df-bd39-40fb-bb61-339fb8b4377f.png)

![image](https://user-images.githubusercontent.com/86935775/127450473-b6fc8a27-7623-4c59-af3f-e73846449130.png)
