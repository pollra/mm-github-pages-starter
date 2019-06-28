---
title: "Vue #3 이벤트 핸들링"
categories:
  - Vue
tags:
  - 이벤트
---

*** 출처 : [Vue.js Tutorial](https://kr.vuejs.org/v2/guide/list.html) ***

#### 이벤트 청취

``v-on`` 디렉티브를 사용하여 DOM 이벤트를 듣고 트리거 될 때 JavaScript 를 실행할 수 있습니다.

```vue
<div id="example-1">
    <button v-on:click="counter += 1">Add 1</button>
    <p> 클릭 횟수 {{counter}}</p>
</div>
```

```vue
let example1 = new Vue({
    el: '#example-1',
    data: {
        counter: 0
    }
})
```

---

###### RESULT <br>

 add 버튼을 클릭하면 클릭횟수가 반응형으로 증가한다.
 
---
---

#### 메소드 이벤트 핸들러

특정 이벤트에 메소드를 연결시켜 이벤트 발생 시 지정한 메소드를 실행

```vue
<div id="example-2">
    <button v-on:click="greet">Greet</button>
    <button v-on:click="say('hi')">say hi</button>
</div>
```

```vue
let example2 = new Vue({
    el: '#example-2',
    data: {
        name: 'Vue.js'
    },
    methods: {
        greet: function (event) {
            alert('Hello '+this.name + '!')
            if( event ){
                alert(event.target.tagName)
            }
        },
        say(message){
            alert(message)
        }
    }
})

<!-- 자바스크립트를 이용한 호출 -->
example2.greet()
example2.say('hi?')

```

---
---

#### 원본 DOM 이벤트 엑세스

```vue
<button v-on:click="warn('ㅇㅅㅇ',$event)">으와아</button>
```

```vue
    methods: {
        warn: function (message, event) {
            if (event) event.preventDefault()
            alert(message)
        }
    }
```

---
---

#### 이벤트 수식어

`v-on` 이벤트에서 사용할 수 있는 이벤트 수식어
이 수식어는 체인이 가능하다.

수식어 | 사용법 | 설명
---|---| ---
`.stop`| `<a v-on:click.stop="doThis"/>` | 이벤트 전파가 중단됩니다.
`.prevent` | `<form v-on:submit.prevent="onSubmit"></form>`<br> OR `<form v-on:submit.prevent></form>` | submit 이벤트가 페이지를 다시 로드하지 않습니다.
`.captrue`|`<div v-on:click.capture="doThis">...</div>`| 내부 엘리먼트를 대상으로 하는 이벤트가 해당 엘리먼트에서 처리되기 전에 여기서 처리합니다.
`.self`|`<div v-on:click.self="doThat">...</div>`| 이벤트 대상이 이 엘리먼트인 경우에만 트리거를 처리합니다.
`.once`|`<a v-on:click.once="doThis"></a>`|클릭이벤트는 최대 한번만 트리거됩니다.
`.passive`| `<div v-on:scroll.passive="onScroll">...</div>` | 스크롤의 기본 이벤트를 취소할 수 없습니다.

---
---

#### 키 수식어

######사용법

`<input v-on:keyup.enter="submit">`


수식어 | 설명
---|---
`.enter`| 엔터키
`.tab`| 탭키
`.delete`| Delete, Backspace 키 모두를 캡처합니다
`.esc`| ESC 키
`.space`| 스페이스바
`.up`| 방향키 위
`.down`| 방향키 아래
`.left`| 방향키 왼쪽
`.right`| 방향키 오른쪽

전역 config.keyCodes 설정<br> 
`Vue.config.keyCodes.f1=112`<br> `v-on:keyup.f1=""` 사용가능

---
---

#### 시스템 수식어

다음 키가 눌러진 경우에만 마우스 또는 키보드 이벤트 리스너를 트리거 합니다.

수식어 | 설명
---|---
`.ctrl`| 컨트롤 키
`.alt` | 알트 키
`.shift`| 쉬프트 키
`.meta`| windows 에선 `windows` 키 / macintosh 에선 `commend` 키

###### 사용법 <br>
ALT + C `<input @keyup.alt.67="clear">`<br>
CTRL + CLICK `<div @click.ctrl="doSomething">Do something</div>`

---
---

#### 정확 수식어

`.exact` 수식어는 정확한 조합이 눌려야만 실행 가능해지는 수식어 입니다.<br>
CTRL + (ALT or SHIFT) 어떤 키와 조합해도 메소드가 실행됨<br>
`<button @click.ctrl="alertAction('ctrl')">ㅇㅅㅇ!!!</button>`

CTRL 키 이외에 다른 키를 누르면 메소드가 실행되지 않음<br>
`<button @click.ctrl.exact="alertAction('ctrl')">ㅇㅂㅇ...</button>`

시스템 키가 눌리지 않은 경우에만 작동<br>
`<button @click.exact="alertAction('ctrl')">ㅇㅁㅇ???</button>`

---
---

### 마우스 버튼 수식어

* `.left`
* `.right`
* `.middle`