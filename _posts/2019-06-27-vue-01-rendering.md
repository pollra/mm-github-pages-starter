---
title: "Vue #01 조건부 렌더링"
categories:
  - Vue
tags:
  - Vue
  - FrontEnd
  - 조건부 렌더링
  
---

*** 출처 : [Vue.js Tutorial](https://kr.vuejs.org/v2/guide/list.html) ***

조건부 렌더링
----

 아래는 여러가지 방법을 이용하여 조건부 렌더링을 하는 방법을 정리했습니다.
 
 코드 바로 아래에 결과로 렌더링 될 HTML 코드를 기록해두었습니다

``<template>``태그 안에는 뷰 템플릿 안의 코드가 들어있고 
``<script>`` 코드 안에는 스크립트 코드가 들어있습니다.
 본래 ``<template>`` 안의 최상위 ``div`` 태그는 하나여야 
 하지만, 본 글에서는 편의를 위해 2개이상의 태그를 사용할 때도 있으니 주의 바랍니다.
 

 - 이중 중괄호를 이용한 방법

###### html

```html
{{#if value}}
  <h1>OK</h1>
{{/if}}
```

###### javaScript

```javascript
let value = true; 
```

---

#### RESULT <br>
```html
<h1>OK</h1>
```

---

---

- v-if 디렉티브를 이용한 방법

```vue
<template>
    <h1 v-if="value">OK</h1>
</template>

<sctipt>
    let value = true;
</sctipt>
```

---

### RESULT<br>
```html
<h1>OK</h1>
```

---

---

- 조건부 그룹 만들기

###### html

```html
    <p>Hi</p>
    <template v-if="value">
        <h1>타이틀</h1>
        <li>목차1</li>
        <li>목차2</li>
    </template>
```

###### javaScript

```javascript
let value = true;
```

#### RESULT<br>
```html
<p>Hi</p> 
<h1>타이틀</h1>
<li>목차1</li>
<li>목차2</li>
```

---

- v-else 디렉티브를 이용한 방법

###### html

```html
<template>
    <div v-if="value">
        value 가 false 이기때문에 이 문장은 안보입니다.
    </div>
    <div v-else>
        이 문장은 보입니다.
    </div>
</template>
```

###### javaScript

```javascript
let value = false;
```

---

#### RESULT<br>

```html
<div>이 문장은 보입니다.</div>
```

---

---

- v-else-if 디렉티브를 이용한 방법

###### html

```html
    <div  v-if="value === 1">
        이 값은 1입니다.
    </div>
    <div  v-if="value === 2">
        2입니다
    </div>
    <div  v-if="value === 3">
        3일겁니다..?
    </div>
```

###### javaScript

```javascript
    let value = 2;
```

---

#### RESULT<br>
```html
<div>2입니다.</div>
```

---

---

- 재사용 엘리먼트 제어

 뷰는 엘리먼트를 효율적으로 렌더링합니다.
 
###### html

```html
    <template v-if="value">
        <label>사용자 이름</label>
        <input placeholder="사용자 이름을 입력">
    </template>
    <template v-else>
        <label>이메일 입력</label>
        <input placeholder="이메일 입력">
    </template>
```

###### javaScript

```javascript
let value = true;
```

---

#### RESULT<br>
```vue
<label>사용자 이름</label>
<input placeholder="사용자 이름을 입력">
```


위에서 value 의 값이 false 로 바뀌게 된다면 이메일 입력 창으로 바뀔것입니다.<br>
```(value 가 뷰의 반응성을 얻은 데이터라고 가정합니다.)``` 그때 뷰는 ``<input>`` 태그를 처음부터 다시 그리는것이 아니라
속성값인 ``placeholder`` 만 바꿔서 렌더링 하게 됩니다.<br>
 기존의 ``<input>`` 태그는 재사용을 하게된다는 말이지요.

 이를 제어하는 방법이 있습니다.
 
###### html
 
```html
    <template v-if="value">
        <label>사용자 이름</label>
        <input placeholder="사용자 이름을 입력" key="username-input">
    </template>
    <template v-else>
        <label>이메일 입력</label>
        <input placeholder="이메일 입력" key="email-input">
    </template>
```

###### javaScript

```javascript
    let value = true;
```

바로 위의 코드에서 바뀐건 ``key`` 속성이 추가되었을 뿐이지만 렌더링방식도 바뀌었습니다.<br>
이제 ``key`` 속성이 있는 ``<input>`` 태그는 처음부터 렌더링 됩니다.

---

- v-show 

v-show 디렉티브를 가지고있는 엘리먼트는 언제나 렌더링되며 ``display`` 속성을 토글합니다.

###### html

```html
<h1 v-show="value">안녕</h1>
```

###### javaScript

```javascript
let value = false
```

#### RESULT<br>
```vue
<h1 style="display: none">안녕</h1>
```