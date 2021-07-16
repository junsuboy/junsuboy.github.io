---
title: "[Javascript] 문서 객체 조작 / 이벤트 사용 함수 정리(1)"
excerpt: "HTML 코드의 문서 객체를 Javascript로 조작하는 다양한 함수 정리"

categories:
  - Javascript
tags:
  - [Javascript]

comments: true
toc: true
toc_sticky: true

date: 2021-07-15
last_modified_at: 2021-07-15
---

# 문서 객체 모델

## 정의

**문서 객체 모델(Document Objects Model)**: 문서 객체를 조합해서 만든 전체적인 형태

## 구조

![image](https://user-images.githubusercontent.com/86935775/125889409-ae0241d3-3af9-4119-ac60-c6e42ba9cc0a.png)

# 문서 객체 조작 함수

## DOMContentLoaded 이벤트

- DOMContentLoaded 이벤트는 웹 브라우저가 문서 객체를 모두 읽고 나서 실행하는 이벤트
- 다음과 같이 코드를 구성하면 DOMContentLoaded 상태가 되었을 때 콜백 함수를 호출

```javascript{.line-numbers}
<!DOCTYPE html>
<html>
 <head>
  <title>DOMContentLoaded</title>
  <script>
    // DOMContentLoaded 이벤트를 연결합니다.
    document.addEventListener('DOMContentLoaded', () => {
      const h1 = (text) => `<h1>${text}</h1>`
      document.body.innerHTML += h1('DOMContentLoaded 이벤트 발생')
    })
  </script>
 </head>
 <body>
 </body>
</html>
```

<br><br>

## 문서 객체 가져오기

- `document.body` 코드를 사용하여 문서의 body 요소 읽기

  - `document.head`
  - `document.body`
  - `document.title`

- `head` 요소와 `body` 요소 내부에 만든 다른 요소들은 다음과 같은 별도의 메소드를 사용
  - `document.querySelector(선택자)`
  - `document.querySelectorAll(선택자)`

![image](https://user-images.githubusercontent.com/86935775/125890569-0ce30b65-8090-4ace-82e2-6f82827614bd.png)

`document.querySelector` **사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
  // 요소를 읽어들입니다.
    const header = document.querySelector(‘h1’)
    // 텍스트와 스타일을 변경합니다.
    header.textContent = 'HEADERS’
    header.style.color = 'white'
    header.style.backgroundColor = 'black'
    header.style.padding = '10px'
  })
</script>
<body>
  <h1></h1>
</body>
```

`document.querySelectorAll` **사용 예시**

```javascript {.line-numbers}
<script>
   document.addEventListener('DOMContentLoaded', () => {
     // 요소를 읽어들입니다.
     const headers = document.querySelectorAll('h1')

     // 텍스트와 스타일을 변경합니다.
     headers.forEach((header) => {
       header.textContent = 'HEADERS’
       header.style.color = 'white’
       header.style.backgroundColor = 'black’
       header.style.padding = '10px'
     })
  })
</script>
<body>
  <h1></h1>
  <h1></h1>
  <h1></h1>
  <h1></h1>
</body>
```

<br>

## 글자 조작하기

- `문서 객체.textContent` : 입력된 문자열을 그대로 기입
- `문서 객체.innerHTML` : 입력된 문자열을 HTML 형식으로 기입

**사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    const a = document.querySelector('#a')
    const b = document.querySelector('#b')

    a.textContent = '<h1>textContent 속성</h1>'
    b.innerHTML = '<h1>innerHTML 속성</h1>'
  })
</script>
<body>
  <div id="a"></div>
  <div id="b"></div>
</body>
```

<br>

## 속성 조작하기

- `문서 객체.setAttribute(속성 이름, 값)` : 특정 속성에 값을 지정
- `문서 객체.getAttribute(속성 이름)` : 특정 속성을 추출

**사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    const rects = document.querySelectorAll('.rect')

    rects.forEach((rect, index) => {
      const width = (index + 1) * 100
      const src = `http://placekitten.com/${width}/250`
      rect.setAttribute('src', src)
    })
  })
</script>
<body>
  <img class="rect">
  <img class="rect">
  <img class="rect">
  <img class="rect">
</body>
```

<br>

## 스타일 조작하기

![image](https://user-images.githubusercontent.com/86935775/125891182-0ee366cb-3ca6-4d6f-bb5e-7901d77fa492.png)

```javascript {.line-numbers}
h1.style.backgroundColor; // 이 형태를 가장 많이 사용
h1.style["backgroundColor"];
h1.style["background-color"];
```

## 문서 객체 생성하기

`document.createElement()` 메소드로 `h1` 태그를 생성하고, 이를 `document.body` 태그 아래에 추가하는 코드

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    // 문서 객체 생성하기
    const header = document.createElement('h1')

    // 생성한 태그 조작하기
    header.textContent = '문서 객체 동적으로 생성하기'
    header.setAttribute('data-custom', '사용자 정의 속성')
    header.style.color = 'white'
    header.style.backgroundColor = 'black'

    // h1 태그를 body 태그 아래에 추가하기
    document.body.appendChild(header)
  })
</script>
<body>
</body>
```

<br>

## 문서 객체 추가/이동/제거

`appendChild()` 메소드는 문서 객체를 자식 객체로 추가할 때 or 이동할 때 사용
문서 객체의 부모(parent)는 언제나 하나여야 하고, 문서 객체를 다른 문서 객체에 추가하면 문서 객체가 이동

<br>

**1. 문서 객체 생성 및 추가**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    // 문서 객체 생성하기
    const header = document.createElement('h1')

    // 생성한 태그 조작하기
    header.textContent = '문서 객체 동적으로 생성하기'
    header.setAttribute('data-custom', '사용자 정의 속성')
    header.style.color = 'white'
    header.style.backgroundColor = 'black'

    // h1 태그를 body 태그 아래에 추가하기
    document.body.appendChild(header)
  })
</script>
<body>
</body>
```

<br>

**2. 문서 객체 이동**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    // 문서 객체 읽어들이고 생성하기
    const divA = document.querySelector('#first')
    const divB = document.querySelector('#second')
    const h1 = document.createElement('h1')
    h1.textContent = '이동하는 h1 태그'

    // 서로 번갈아가면서 실행하는 함수를 구현합니다.
    const toFirst = () => {
      divA.appendChild(h1)
      setTimeout(toSecond, 1000)
    }
    const toSecond = () => {
      divB.appendChild(h1)
      setTimeout(toFirst, 10000)
    }
    toFirst()
  })
</script>

<body>
  <div id="first">
    <h1>첫 번째 div 태그 내부</h1>
  </div>
  <hr>
<div id="second">
    <h1>두 번째 div 태그 내부</h1>
  </div>
</body>
```

<br>

**3. 문서 객체 제거**
`removeChild()` 메소드: 문서 객체를 제거
`부모 객체.removeChild(자식 객체)`

- `appendChild()` 메소드 등으로 부모 객체와 이미 연결이 완료된 문서 객체의 경우 `parentNode` 속성으로 부모 객체에 접근할 수 있으므로, 일반적으로 어떤 문서 객체를 제거할 때는 다음과 같은 형태의 코드를 사용
  `문서 객체.parentNode.removeChild(문서 객체)`

**사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    setTimeout(() => {
      const h1 = document.querySelector('h1')

      h1.parentNode.removeChild(h1)
      // document.body.removeChild(h1)
    }, 3000)
  })
</script>
<body>
  <hr>
  <h1>제거 대상 문서 객체</h1>
  <hr>
</body>
```

<br><br>

## 이벤트 설정하기

`addEventListener()` 메소드
`문서 객체.addEventListener(이벤트이름, 콜백함수, 캡처여부)`

**사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    let counter = 0
    const h1 = document.querySelector('h1')

    h1.addEventListener('click', (event) => {
      counter++
      h1.textContent = `클릭 횟수: ${counter}`
    })
  })
</script>
<style>
  h1 {
    /* 클릭을 여러 번 했을 때
    글자가 선택되는 것을 막기 위한 스타일 */
    user-select: none;
  }
</style>
<body>
  <h1>클릭 횟수: 0</h1>
</body>
```

<br>

`removeEventListener()` 메소드
`문서 객체.removeEventListener(이벤트 이름, 이벤트 리스너)`

**사용 예시**

```javascript {.line-numbers}
<script>
  document.addEventListener('DOMContentLoaded', () => {
    let counter = 0
    let isConnect = false

    const h1 = document.querySelector('h1')
    const p = document.querySelector('p')
    const connectButton = document.querySelector('#connect')
    const disconnectButton = document.querySelector('#disconnect')

    const listener = (event) => {
    h1.textContent = `클릭 횟수: ${counter++}`
    }

    connectButton.addEventListener('click', () => {
    if (isConnect === false) {
      h1.addEventListener('click', listener)
      p.textContent = '이벤트 연결 상태: 연결’
      isConnect = true
    }
  })
    disconnectButton.addEventListener('click', () => {
      if (isConnect === true) {
        h1.removeEventListener('click', listener)
        p.textContent = '이벤트 연결 상태: 해제'
        isConnect = false
      }
    })
  })
</script>
```

```html
<head>
  <style>
    h1 {
      /* 클릭을 여러 번 했을 때
           글자가 선택되는 것을 막기 위한 스타일 */
      user-select: none;
    }
  </style>
</head>
<body>
  <h1>클릭 횟수: 0</h1>
  <button id="connect">이벤트 연결</button>
  <button id="disconnect">이벤트 제거</button>
  <p>이벤트 연결 상태: 해제</p>
</body>
```
