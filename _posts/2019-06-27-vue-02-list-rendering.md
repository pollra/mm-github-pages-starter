---
title: "Vue #01 렌더링"
categories:
  - posts
tags:
  - Vue
  - 뷰
  - FrontEnd
  - 리스트 렌더링
---

#Vue #02

리스트 렌더링
---

 아래는 여러가지 방법을 이용하여 리스트 렌더링을 하는 방법을 정리했습니다.
 
 코드 바로 아래에 결과로 렌더링 될 HTML 코드를 기록해두었습니다

``<template>``태그 안에는 뷰 템플릿 안의 코드가 들어있고 
``<script>`` 코드 안에는 스크립트 코드가 들어있습니다.
 본래 ``<template>`` 안의 최상위 ``div`` 태그는 
 하나여야 하지만, 본 글에서는 편의를 위해 2개이상의 태그를 사용할 때도 있으니 주의 바랍니다.
 
- v-for 

######html

```vue
<ul v-for="(user, index) in arrUsers">
    <li>index</li>
    <li>{{user.name}}</li>
    <li>{{user.age}}</li>
</ul>
```

######data

```javascript
let arrUser = [
        {name:"Mark Alan Ruffalo", age:51},
        {name:"Robert John Downey Jr", age:54}
    ]
```

{% captrue notice-1 %}

####RESULT

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

{% endcaptrue %}

<div class="notice">{{ notice-1 | markdownify }}</div>

