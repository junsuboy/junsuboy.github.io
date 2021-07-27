---
title: "[jQuery] jQuery 이벤트 등록 방식"
excerpt: "그룹 이벤트 등록 메서드 및 이벤트 제거 메서드"

categories:
  - jQuery
tags:
  - [Javascript, jQuery]

comments: true
toc: true
toc_sticky: true

date: 2021-07-22
last_modified_at: 2021-07-22
---

# on() 메서드 - 그룹 이벤트 등록 메서드

`on()` 메서드는 그룹 이벤트 등록 메서드 중 가장 빈번하게 쓰이는 메서드입니다.

사용 방법을 알아봅시다.

<br><br>

- `on()` 메서드 등록 방식 1

```javascript
$("이벤트 대상 선택").on("이벤트 종류1 이벤트 종류2 ... 이벤트 종류n",
function(){
    javascript 코드;
});
```

- `on()` 메서드 등록 방식 2

```javascript
$("이벤트 대상 선택").on({
    "이벤트 종류1 이벤트 종류2 ... 이벤트 종류n" : function(){
        javascript 코드;
    }
})
```

- `on()` 메서드 등록 방식 3

```javascript
$("이벤트 대상 선택").on({
    "이벤트 종류1" : function() { javascript 코드; 1},
    "이벤트 종류2" : function() { javascript 코드; 2},
          ...
    "이벤트 종류n" : function() { javascript 코드; n},
})
```

<br><br><br>

# 그 외 다양한 그룹 이벤트 등록 메서드

> > 그룹 이벤트 등록 메서드 종류

- `on()` : 이벤트 대상 요소에 2개 이상의 이벤트를 등록합니다. 사용 방식에 따라 이벤트를 등록한 이후에도 동적으로 생성되거나 복제된 요소에도 이벤트가 적용됩니다.

- `bind()` : 이벤트 대상 요소에 2개 이상의 이벤트를 등록합니다.

- `delegate()` : 선택한 요소의 하위 요소에 이벤트를 등록합니다. 이벤트를 등록한 이후에도 동적으로 생성되거나 복제된 요소에도 이벤트가 적용됩니다.

- `one()` : 이벤트 대상 요소에 1개 이상의 이벤트를 등록합니다. 지정한 이벤트가 1회 발생하고 자동으로 해제됩니다.

<br><br><br>

# 이벤트 제거 메서드

> > 이벤트 제거 메서드의 종류

- `off()` : `on()` 메서드로 등록한 이벤트를 제거합니다.
- `unbind()` : `bind()` 메서드로 등록한 이벤트를 제거합니다.
- `undelegate()` : `delegate()` 메서드로 등록한 이벤트를 제거합니다.
