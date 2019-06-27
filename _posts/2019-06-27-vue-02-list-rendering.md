---
title: "Vue #02 리스트 렌더링"
categories:
  - Vue
tags:
  - Vue
  - FrontEnd
  - 리스트 렌더링
---

리스트 렌더링
---

 아래는 여러가지 방법을 이용하여 리스트 렌더링을 하는 방법을 정리했습니다.
 
 코드 바로 아래에 결과로 렌더링 될 HTML 코드를 기록해두었습니다

``<template>``태그 안에는 뷰 템플릿 안의 코드가 들어있고 
``<script>`` 코드 안에는 스크립트 코드가 들어있습니다.
 본래 ``<template>`` 안의 최상위 ``div`` 태그는 
 하나여야 하지만, 본 글에서는 편의를 위해 2개이상의 태그를 사용할 때도 있으니 주의 바랍니다.
 
- v-for 

###### html

```vue
<ul v-for="(user, index) in arrUsers"><!-- in 대신 of 사용 가능-->
    <li>{{index}}</li>
    <li>{{user.name}}</li>
    <li>{{user.age}}</li>
</ul>
```

###### data

```javascript
let arrUser = [
        {name:"Mark Alan Ruffalo", age:51},
        {name:"Robert John Downey Jr", age:54}
    ]
```

---

#### RESULT

```vue
<ul>
  <li>0</li>
 <li>Mark Alan Ruffalo</li>
 <li>51</li>
</ul>
<ul>
  <li>1</li>
  <li>Robert John Downey Jr</li>
  <li>54</li>
</ul>
```

---

---

- v-for 와 객체

###### html

```vue
<ul v-for="obj in object_h"><!-- in 대신 of 사용 가능-->
    <li>{{obj}}</li>
</ul>
```

###### data

```javascript
let object_h={name:"Mark Alan Ruffalo", age:51, starring:"avengers"}
```

---

#### RESULT

```vue

<ul>
    <li>Mark Alan Ruffalo</li>
    <li>51</li>
    <li>avengers</li>
</ul>

```

---

---

###### html

```vue
<ul v-for="(val, key) in object_h"><!-- in 대신 of 사용 가능-->
    <li>{{key}}: {{val}}</li>
</ul>
```

###### data

```javascript
let object_h={name:"Mark Alan Ruffalo", age:51, starring:"avengers"}
```

---

#### RESULT

```vue

<ul>
    <li>Mark Alan Ruffalo</li>
    <li>51</li>
    <li>avengers</li>
</ul>

```

---

---

객체를 반복할 때 순서는 Object.keys()의 키 나열 순서에 따라 결정됩니다. 이 순서는 JavaScript 엔진 구현간에 일관적이지는 않습니다.
{: .notice--danger}

