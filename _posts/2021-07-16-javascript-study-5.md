---
title: "[Javascript] 문서 객체 조작 / 이벤트 사용 함수 정리(2)"
excerpt: "HTML 코드의 문서 객체를 Javascript로 조작하는 다양한 함수 정리"

categories:
  - Javascript
tags:
  - [Javascript]

comments: true
toc: true
toc_sticky: true

date: 2021-07-16
last_modified_at: 2021-07-16
---

## 이벤트 모델

- 표준 이벤트 모델 : `addEventListener()`

```javascript
document.body.addEventListener("keyup", () => {});
```

- 고전 이벤트 모델 : 문서 객체가 갖고 있는 on◯◯으로 시작하는 속성에 함수를 할당해서 이벤트를 연결

```javascript
document.body.onkeyup = (event) => {};
```

- 인라인 이벤트 모델 : on◯◯으로 시작하는 속성을 HTML 요소에 직접 넣어서 이벤트를 연결

```javascript
<script>
  const listener = (event) => {

  }
</script>
<body onkeyup="listener(event)">
</body>
```

<br><br>

## 키보드 이벤트

![image](https://user-images.githubusercontent.com/86935775/125913165-070302e3-ad19-4d9c-848d-555534c9e94e.png)

**사용 예시**

```javascript
<script>
  document.addEventListener('DOMContentLoaded', () => {
    const textarea = document.querySelector('textarea')
    const h1 = document.querySelector('h1')
    textarea.addEventListener('keyup', (event) => {
      const length = textarea.value.length
      h1.textContent = `글자 수: ${length}`
    })
  })
</script>
<body>
  <h1></h1>
  <textarea></textarea>
</body>
```

<br><br>

## 키보드 키 속성 사용하기

![image](https://user-images.githubusercontent.com/86935775/125913386-60c96cab-db2e-4288-96ad-3eb063a59877.png)

- code 속성은 입력한 키를 나타내는 문자열이 들어 있고, altKey, ctrlKey, shiftKey 속성은 해당 키를 눌렀는지 불 자료형 값이 들어 있음

**사용 예시**

```javascript
<script>
  document.addEventListener('DOMContentLoaded', () => {
    const h1 = document.querySelector('h1')
    const print = (event) => {
      let output = ''
      output += `alt: ${event.altKey}<br>`
      output += `ctrl: ${event.ctrlKey}<br>`
      output += `shift: ${event.shiftKey}<br>`
      output += `code: ${typeof(event.code) !== 'undefined' ?
        event.code : event.keyCode}<br>`
      h1.innerHTML = output
    }

    document.addEventListener('keydown', print)
    document.addEventListener('keyup', print)
  })
</script>
<body>
  <h1></h1>
</body>
```

<br><br>

## 이벤트 발생 객체에 접근할 수 없는 경우

- 이벤트 리스너 내부에서 어떤 변수에 접근할 수 없는 경우
- 다음 코드에서는 listener() 함수 내부에서 textarea 변수에 접근할 수 없어 오류가 발생
  - 이벤트 리스너를 외부로 빼낸 경우

```javascript
<script>
  const listener = (event) => {
    const length = textarea.value.length
    h1.textContent = `글자 수: ${length}`
  }

  document.addEventListener('DOMContentLoaded', () => {
    const textarea = document.querySelector('textarea’)
    const h1 = document.querySelector('h1')
    textarea.addEventListener('keyup', listener)
  })
</script>
```

**문제해결 1 : event.currentTarget 속성을 사용**

```javascript
<script>
  const listener = (event) => {
    const length = event.currentTarget.value.length
    h1.textContent = `글자 수: ${length}`
  }
  document.addEventListener('DOMContentLoaded', () => {
    const textarea = document.querySelector('textarea')
    const h1 = document.querySelector('h1')
    textarea.addEventListener('keyup', listener)
  })
</script>
```

**문제해결 2 : this 키워드를 사용**

```javascript
<script>
  const listener = function (event) {
    const length = this.value.length
    h1.textContent = `글자 수: ${length}`
  }
  document.addEventListener('DOMContentLoaded', () => {
    const textarea = document.querySelector('textarea')
    const h1 = document.querySelector('h1')
    textarea.addEventListener('keyup', listener)
  })
</script>
```

<br><br>

## 기본 이벤트 막기

- 기본 이벤트: 어떤 이벤트가 발생했을 때 웹 브라우저가 기본적으로 처리해주는 것

**사용 예시 - 이미지 마우스 오른쪽 버튼 클릭 막기**

```javascript
<script>
  document.addEventListener('DOMContentLoaded', () => {
    const imgs = document.querySelectorAll('img')

    imgs.forEach((img) => {
      img.addEventListener('contextmenu', (event) => {
        event.preventDefault()
      })
    })
  })
</script>
<body>
  <img src="http://placekitten.com/300/300" alt="">
</body>
```

**사용 예시 - 체크 때만 링크 활성화하기**

```javascript
<script>
  document.addEventListener('DOMContentLoaded', () => {
    let status = false

    const checkbox = document.querySelector('input')
    checkbox.addEventListener('change', (event) => {
      status = event.currentTarget.checked
    })

    const link = document.querySelector('a')
    link.addEventListener('click', (event) => {
      if (!status) {
        event.preventDefault
      }
    })
  })
</script>
<body>
  <input type="checkbox">
  <span>링크 활성화</span>
  <br>
  <a href="http://google.co.kr">구글</a>
</body>
```

## LocalStorage 객체

- 웹 브라우저에 데이터를 저장하는 localStorage 객체와 활용
  - `localStorage.getItem(키)`: 저장된 값을 추출. 없으면 undefined가 나옴. 객체의 속성을 추출하는 일반적인 형태로 localStorage.키 또는 localStorage[키] 형태로 사용 할 수도 있음
  - `localStorage.setItem(키, 값)`: 값을 저장이전과 마찬가지로 객체에 속성을 지정하는 일반적인 형태를 사용할 수도 있음
  - `localStorage.removeItem(키)`: 특정 키의 값을 제거
  - `localStorage.clear()`: 저장된 모든 값을 제거
