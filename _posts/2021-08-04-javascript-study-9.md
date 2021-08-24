---
title: "[Javascript] 화살표 함수 (arrow function)"
excerpt: "화살표 함수 기본적인 사용 방법"

categories:
  - Javascript
tags:
  - [Javascript]

comments: true
toc: true
toc_sticky: true

date: 2021-08-04
last_modified_at: 2021-08-04
---


화살표 함수는 ES6문법입니다. function 키워드 사용해서 함수를 만든 것보다 간단히 함수를 표현할 수 있습니다. 화살표 함수는 항상 익명입니다.


```javascript
// 일반 함수
var foo = function () { console.log("foo") }; // foo

// 화살표 함수
var bar = () => console.log("bar"); // bar
```

<br><br><br>


# 화살표 함수의 기본 문법

```javascript
// 매개변수가 없는 경우
var foo = () => console.log('bar');
foo(); // bar

// 매개변수가 하나인 경우
var foo = x => x;
foo('bar'); // bar

// 매개변수가 여려개인 경우
var foo = (a, b) => a + b; // 간단하게 한줄로 표현할 땐 "{}" 없이 값이 반환됩니다.
foo(1, 2); // 3

var foo = (a, b) => { return a + b }; 
foo(1, 2); // 3

var foo = (a, b) => { a + b }; // "{}"를 사용했는데 return이 없을 때 
foo(1, 2); // undefined

var foo = (a, b) => { // 여러줄 썼을 때
	var c = 3;
	return a + b + c;
}
foo(1, 2, 3) // 6
/*
"{}"를 사용하면 값을 반환할 때 return을 사용해야합니다.
"{}"를 사용하지 않으면 undefied를 반환합니다.
"{}"을 사용할 때는 여러줄을 썼을 때 사용합니다.
*/

// 객체를 반환할 때
var foo = () => ( { a: 1, b: 2, c: 3 } );
foo(); // { a: 1, b: 2, c: 3 };
```

<br>

콜백 함수에서도 사용할 수 있습니다.

<br>

```javascript
// ES5
var numbers = [1, 4, 9];
var oddArr = numbers.filter(function (x) { return x % 2 !== 0;});
console.log(oddArr); // [1, 9]
```

```javascript
// ES6
var numbers = [1, 4, 9];
var oddArr = numbers.filter( x => (x % 2) !== 0 );
console.log(oddArr); // [1, 9]
```

<br><br><br>

# 화살표 함수 this

일반 함수와 화살표 함수의 차이점이 있습니다. 일반함수가 전역 컨텍스트에서 실행될 때 this가 정의합니다. 화살표함수는 this를 정의하지 않습니다.

함수의 내부함수, 콜백함수에 사용되는 this는 window입니다.


```javascript
let cat = {
	  sound: "meow",
  	soundPlay: function () {
      	console.log(this) // 가.
		  setTimeout(function () {
			console.log(this) // 나.
			console.log(this.sound); // 다.
		}, 1000);
    }
}

cat.soundPlay();
// 가. cat {sound: "meow", soundPlay: ƒ}
// 나. window
// 다. undefined -----> undefined인 이유는 window에 sound가 없어서입니다.
```

<br>

일반함수에서의 적절한 this를 전달하는 방법이 있습니다.


<br>

```javascript
// 함수안에 that 변수를 선언하기
let cat = {
	sound: "meow",
  	soundPlay: function () {
      	let that = this // that 사용
		setTimeout(function () {
			console.log(that.sound);
		}, 1000);
    }
}

cat.soundPlay();
// 1초 후에 ... "meow"

// bind 사용하기
let cat = {
	sound: "meow",
  	soundPlay: function () {
		setTimeout(function () {
			console.log(this.sound);
		}.bind(this), 1000); // bind 사용
    }
}

cat.soundPlay();
// 1초 후에 ... "meow"
```

<br>

화살표 함수를 사용해보겠습니다.

<br>

```javascript
let cat = {
	sound: "meow",
  	soundPlay: function () {
		setTimeout(() => {
			console.log(this.sound);
		}, 1000);
    }
}

cat.soundPlay();
// 1초 후에 ... "meow"
```

이게 가능한 이유는 클로저 함수처럼 바깥의 함수에 접근해서 this를 사용합니다.

<br><br>

[참고 링크]

<https://poiemaweb.com/es6-arrow-function>

<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/애로우_펑션>