---
title: "[React.js] prop-types 사용 방법"
excerpt: "prop-types를 활용하여 props가 올바르게 전달되었는지 확인하는 방법"

categories:
  - react
tags:
  - [Javascript, react]

comments: true
toc: true
toc_sticky: true

date: 2021-07-29
last_modified_at: 2021-07-29
---

# prop-types Library란?

컴포넌트 props에 타입 확인을 할 수 있는 Library입니다.

터미널에서 앱이 위치한 경로에 다음과 같은 명령어로 설치할 수 있습니다.

`npm i prop-types`

<br><br>

# 사용법

prop-types의 여러가지 활용법을 알아봅시다

<br><br>

## props의 자료형 확인하기

설치된 prop-types를 다음과 같이 import합니다.

```javascript
import PropTypes from "prop-types";
```

다음과 같이 `function Food`에 **name, picture, rating이라는 props에 각각 string이 전달되었는지** 확인합니다.

```javascript
import React from "react";
import PropTypes from "prop-types";

const foodILike = [
  {
    id: 1,
    name: "kimchi",
    image:
      "https://kstory365.files.wordpress.com/2015/01/kimchi-01-cabbage.jpg",
    rating: 3.3,
  },
  {
    id: 2,
    name: "ramen",
    image:
      "https://i.huffpost.com/gen/1410937/thumbs/o-RAMEN-facebook.jpg#Ramen%202000x1000",
    rating: 4.4,
  },
  {
    id: 3,
    name: "samgyeopsal",
    image:
      "https://www.gildedgingerbread.com/wp-content/uploads/2017/08/Samgyeopsal-1.jpg",
    rating: 5.5,
  },
  {
    id: 4,
    name: "kimbap",
    image:
      "https://www.maangchi.com/wp-content/uploads/2007/08/gimbap_plate.jpg",
    rating: 5.0,
  },
  {
    id: 5,
    name: "bibimbap",
    image:
      "https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Dolsot-bibimbap.jpg/1200px-Dolsot-bibimbap.jpg",
    rating: 4.1,
  },
];

function Food({ name, picture, rating }) {
  return (
    <div>
      <h2>I like {name}</h2>
      <h4>{rating}/5.0</h4>
      <img src={picture} alt={name} />
    </div>
  );
}

Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.string.isRequired,
};

function App() {
  return (
    <div className="App">
      {foodILike.map((dish) => (
        <Food
          key={dish.id}
          name={dish.name}
          picture={dish.image}
          rating={dish.rating}
        />
      ))}
    </div>
  );
}

export default App;
```

[props type 확인 구문]

```javascript
Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.string.isRequired,
};
```

현재 props `rating`은 string이 아닌 number type이므로

사이트 console 창에는 아래와 같이 에러가 발생합니다.

![image](https://user-images.githubusercontent.com/86935775/127464836-eb02c989-9d3e-4d95-97c6-fc8f3df21804.png)

위 에러는 propTypes 사용부에 아래와 같이 수정함으로써 해결할 수 있습니다.

즉, props가 number type인지 확인하는 구문으로 사용하는 것입니다.

```javascript
Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired,
};
```

위와 같이 수정하면 해당 오류는 사라집니다.

<br><br>

## props가 제대로 전달되었는지 확인하기

다음과 같이 picture를 argument로서 전달하는 대신, image라는 정의되지 않은 argument로 props를 전달 시도합니다.

```javascript
import React from "react";
import PropTypes from "prop-types";

const foodILike = [
  {
    id: 1,
    name: "kimchi",
    image:
      "https://kstory365.files.wordpress.com/2015/01/kimchi-01-cabbage.jpg",
    rating: 3.3,
  },
  {
    id: 2,
    name: "ramen",
    image:
      "https://i.huffpost.com/gen/1410937/thumbs/o-RAMEN-facebook.jpg#Ramen%202000x1000",
    rating: 4.4,
  },
  {
    id: 3,
    name: "samgyeopsal",
    image:
      "https://www.gildedgingerbread.com/wp-content/uploads/2017/08/Samgyeopsal-1.jpg",
    rating: 5.5,
  },
  {
    id: 4,
    name: "kimbap",
    image:
      "https://www.maangchi.com/wp-content/uploads/2007/08/gimbap_plate.jpg",
    rating: 5.0,
  },
  {
    id: 5,
    name: "bibimbap",
    image:
      "https://upload.wikimedia.org/wikipedia/commons/thumb/4/44/Dolsot-bibimbap.jpg/1200px-Dolsot-bibimbap.jpg",
    rating: 4.1,
  },
];

function Food({ name, picture, rating }) {
  return (
    <div>
      <h2>I like {name}</h2>
      <h4>{rating}/5.0</h4>
      <img src={picture} alt={name} />
    </div>
  );
}

Food.propTypes = {
  name: PropTypes.string.isRequired,
  picture: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired,
};

function App() {
  return (
    <div className="App">
      {foodILike.map((dish) => (
        <Food
          key={dish.id}
          name={dish.name}
          image={dish.image}
          rating={dish.rating}
        />
      ))}
    </div>
  );
}

export default App;
```

`function Food`에서는 name, picture, rating을 argument로서 전달받으려고 하고 있는데, `function App`에서는 image를 argument로 사용하여 **다음과 같이 이미지는 정상적으로 로드되지 않고, 그림과 같은 오류**가 발생합니다.

![image](https://user-images.githubusercontent.com/86935775/127465846-0cf06f78-2803-43db-b792-d30a066db3ff.png)

![image](https://user-images.githubusercontent.com/86935775/127465450-97debfc6-7283-4ea3-a541-afb0043b0540.png)

위와 같이 picture가 정상적으로 전달되지 않았다는 것을 확인할 수 있고, 이는 앱이 복잡해지고 커질수록 오류를 찾는 데에 있어서 유용하게 활용될 수 있을 것입니다.

물론 오류가 처음부터 없는게 최고겠지만요. 😂

<br><br>

[참조 링크 - React PropTypes와 함께 하는 타입 확인](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)
