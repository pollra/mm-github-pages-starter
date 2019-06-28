---
title: "Vue #02 리스트 렌더링"
categories:
  - Vue
tags:
  - Vue
  - FrontEnd
  - 리스트 렌더링
---

*** 출처 : [Vue.js Tutorial](https://kr.vuejs.org/v2/guide/list.html) ***

리스트 렌더링
---

 아래는 여러가지 방법을 이용하여 리스트 렌더링을 하는 방법을 정리했습니다.
 
 코드 바로 아래에 결과로 렌더링 될 HTML 코드를 기록해두었습니다

``<template>``태그 안에는 뷰 템플릿 안의 코드가 들어있고 
``<script>`` 코드 안에는 스크립트 코드가 들어있습니다.
 본래 ``<template>`` 안의 최상위 ``div`` 태그는 
 하나여야 하지만, 본 글에서는 편의를 위해 2개이상의 태그를 사용할 때도 있으니 주의 바랍니다.
 
## v-for 


#### key

Vue 는 렌더링된 엘리먼트 목록을 갱신할 때 기본적으로
 "in-place patch" 전략을 사용합니다.
기존에 있는 데이터가 수정되었을 경우 DOM 요소를 움직여서
 HTML 코드를 정렬하는것이 아니라 DOM 요소는 가만히 있고
 안의 데이터만 움직이는것입니다.
 
 목록의 출력 결과가 하위 컴포넌트 상태 또는 임시 DOM 상태
 (예: 폼 input)에 의존하지 않는 경우에 적합합니다.

 vue 에서 DOM 요소를 추적할 수 있게 v-for 의 각 항목들에 대해 
 고유한 key 값을 전달해주어야 합니다.
 
 key 값은 객체나 배열이 같은 기본타입이 아닌 값으로 하면 안됩니다.
 문자열이나 숫자를 사용하는것이 적합합니다.

---
---

###### html

```vue
<ul v-for="(user, index) in arrUsers" :key="user"><!-- in 대신 of 사용 가능-->
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

#### v-for 와 객체

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

***객체를 반복할 때 순서는 Object.keys()의 키
 나열 순서에 따라 결정됩니다. 이 순서는 JavaScript
  엔진 구현간에 일관적이지는 않습니다.***

---
---

 
#### 변이 메소드

 다음의 메소드를 사용하여 Vue 의 배열을 변이 시켜 뷰 갱신을 트리거할 수 있습니다.
 
* push()
* pop()
* shift()
* unshift()
* sort()
* reverse()

 다음 사이트에 가면 변이 메소드를 실습해 볼 수 있습니다.
 [링크](https://kr.vuejs.org/v2/guide/list.html#%EA%B8%B0%EB%B3%B8-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95)
 <br>
 해당 페이지에서 콘솔(``F12``)을 열고 ``items`` 배열에 
 ``push`` 메소드를 이용하여 ``message`` 값을 추가할 수 있습니다. 
 ``example1.items.push({message:'Baz'})``

#### 주의사항

데이터를 업데이트 할 때 JavaScript 의 한계로 
Vue 의 반응성을 이용하지 못하게 되는 경우가 존재합니다.

###### Vue.set 을 이용한 배열을 업데이트할때 잘못된 예

1. 인덱스로 배열에 있는 데이터를 직접 설정 : ``vm.items[indexOfItem] = newValue``
2. 배열의 길이를 수정 : ``vm.items.length = newLength``
3. 반응형 속성을 동적으로 추가 : ``vm.a = 1``

###### 해결방법

1. ``Vue.set(example1.items, indexOfItem, newValue)`` <br> ``example1.items.splice(indexOfItem, 1, newValue)``

2. ``example1.items.splice(newLength)``

3. 객체에 새로운 속성 추가<br>
   ``Vue.set(vm.userProfile, 'age', 27)``<br>
   인스턴스 메소드를 사용한 속성 추가<br>
   ``vm.$set(this.userProfile, 'age', 27)``<br>
   객체를 이용한 새로운 속성을 기존의 객체에 추가<br>
   ``this.userProfile = Object.assign({}, this.userProfile, {
    age:27, favoriteColor:'Vue Green'
   })``

---
---

#### 필터링 / 정렬된 결과 표시

배열의 데이터를 변경하지 않고 특정 기준으로 정렬해야할 때
(계산된 속성을 사용할 수 있는 상황)

```vue
<li v-for="n in evenNumbers">{{n}}</li>
```

```vue
data:{
    numbers:[1, 2, 3, 4, 5]
},
computed:{
    evenNumbers: function(){
      return this.numbers.filter(function (number){
        return number % 2 === 0
    })
  }
}
```

```vue
<li v-for="n in even(numbers)">{{n}}</li>
```

```vue
data:{
    numbers:[1, 2, 3, 4, 5]
},
methods:{
    even: function (numbers) {
        return numbers.filter(function (number){
            return number % 2 === 0
        })
    }
}
```

---
---

#### Range v-for

```vue
<div>
    <span v-for="n in 10">{{n}}</span>
</div>
```

###### RESULT <br>
``<span>1</span>``<br>
``<span>2</span>``<br>
``<span>3</span>``<br>
``<span>4</span>``<br>
``<span>5</span>``<br>
``<span>6</span>``<br>
``<span>7</span>``<br>
``<span>8</span>``<br>
``<span>9</span>``<br>
``<span>10</span>``

---
---

#### v-for 와 v-if

> 동일한 노드에 두가지 모두 있다면 v-if 가 v-for 보다 높은 우선순위를 가짐.
> <br>다음의 코드는 v-if 실행 이후 v-for 실행됨. 자바의 
> for(int i = 1;i % 2 == 0 && i <= 10; i++) 와 같은 동작을 보임

```vue
<li v-for="n in 10" v-if="n % 2 === 0">{{n}}</li>
```

###### RESTUL <br>

```vue
<li>2</li>
<li>4</li>
<li>6</li>
<li>8</li>
<li>10</li>
```

---
---