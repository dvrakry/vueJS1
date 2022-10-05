# Vue 강의노트

### 데이터바인딩::

```jsx
<script>
	export default {
  name: 'App',
  data(){
    return {
      메뉴들: ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
</script>

위에 메뉴들(ARRAY)를 데이터로 저장해 바인딩 할 수 있음
바인딩 한 데이터는 

<h4>{{products[0]}}</h4> -> 이렇게 바인딩 하여 사용함 {{ }}
```

- HTML 태그안의 속성에 데이터 바인딩 할땐  **:**  (콜론을 붙여줘야함)

```jsx
<img :src="원룸들[0].image" class="room-img">
```

### For 반복문:

```jsx
<template>
 <div v-for="(a,i) in 원룸들" :key="i"> ->원룸들 갯수만큼 반복문을 돌림
    <img :src="원룸들[i].image" class="room-img">
    <h4>{{원룸들[i].title}}</h4>
    <p>{{원룸들[i].price}}원</p>
 </div>
</template>
-> 원룸들[i] = a 랑 같음 원룸들[i]의 데이터들을 작명한게 a 이기 때문에
	
<script>
	export default {
  name: 'App',
  data(){
    return {
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
</script>

	- 반복문의 경우 v-for 를 사용하며 :key 도 함께 사용해줘야함.
	- Array를 통해 key 값을 사용하려면 i 값을 함께 바인딩 해줘야함
```

### **Vue 이벤트 핸들러 Click:**

- ○ v-on:click="" / @click=""

```jsx
<button @click="신고수++">허위매물신고</button> 
<span>신고수 : {{신고수}}</span>

```

### Vue 함수:

```jsx
data(){
    return {
      신고수 : 0,
		}
	}
methods : {
    increase(){
      this.신고수 += 1;  -> 여기서 위에 데이터에 있는 신고수를 사용하기 위해선
					 반드시 this.신고수로 작성해야함(그렇지않으면 오류)
    }
  },

-Vue에서 함수를 만들고 싶으면 methods :{함수(){}} 안에 만들면됨
-함수를 쓸땐 @click="increase" 로 사용하면 됨 increase() (X) 안됨/ 괄호붙이면 안됨
```

### 동적 UI 만드는 법:

1.  UI의 현재 상태를 데이터에 저장해둠
2. 데이터에 따라 UI가 어떻게 보일지 작성

---

- 데이터 저장

```jsx
export default {
  name: 'App',
  data(){
    return {
      모달창열렸니 : false, -> 여기에 모달창 상태를 저장
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
```

- 모달창

```jsx
	<div class="black-bg" v-if="모달창열렸니 == true"> 
												*v-if는 조건식이 참일때만 이 코드를 보여줌
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
    </div>
  </div>
```

- 클릭시 데이터 상태 변경

```jsx
	<div>
    <img src="./assets/room0.jpg" class="room-img">
    <h4 @click="모달창열렸니 = true">{{products[0]}}</h4>
		->여기서 클릭시 데이터에 저장된 [모달창 열렸니]가 true로 변하면서
			모달창 v-if 가 true가 되면서 코드가 보여짐
		-> 모달창열렸니 = true / 이 코드는 모달창열렸니에 true값을
                            넣는다는 뜻임(== true 와 다름)
    <p>50 만원</p>
    <button @click="신고수[0]++">허위매물신고</button> 
    <span>신고수 : {{신고수[0]}}</span>
  </div>
```

### Import/Export 문법:

> 너무 많은 양의 데이터를 담을 때 다른 JS 파일로 생성해서 불러오는 문법
> 
- 기본(App.vue 에서 one.js 에 있는 변수를 사용하고 싶을때)
- oneroom.js

```jsx
export default [{
    id : 0,
    title: "Sinrim station 30 meters away",
    image: "https://codingapple1.github.io/vue/room0.jpg",
    content: "18년 신축공사한 남향 원룸 ☀️, 공기청정기 제공",
    price: 340000
    },
}];
```

- App.vue

```jsx
<template>
	<div>
    <img src="./assets/room0.jpg" class="room-img">
    <h4>{{원룸들[0].title}}</h4>
    <p>{{원룸들[0].price}}원</p>
  </div>
</template>
<script>

import data from './assets/oneroom.js';

export default {
  name: 'App',
  data(){
    return {
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
</script>
```

### Component 컴포넌트:

> 컴포넌트를 사용하는 이유는 길거나 복잡한 HTML을 삽입하거나 한 HTML을 여러군데에 사용할 경우 코드 간결화를 위해 사용함
> 

- Discount.vue 생성

```jsx
<template>
    <!-- 할인배너 -->
  <div class="discount">
    <h4>지금 결제하면 20% 할인</h4>
  </div>
</template>

<script>
export default {
    name : 'Discount', **1.컴포넌트 이름 등록**

}
</script>

<style>

</style>
```

- App.vue

```jsx
<template>
	<Discount/> 4. 등록된 컴포넌트 사용
</template>

<script>
	import data from './assets/oneroom.js';
	import Discount from './Discount.vue';  **2.불러오기**

export default {
  name: 'App',
  data(){
    return {
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase(){
      this.신고수 += 1
    }
  },
  components: {
    Discount : Discount, **3.컴포넌트 등록**
  }
}
</script>
```

## Props: 부모/자식

> 자식 컴포넌트가 부모가 갖고 있는 데이터를 쓰려면 props로 데이터를 전송해야함
> 
- props로 자식에게 데이터 보내는법

→ 데이터 보내고 / 등록하고 / 사용

→ props로 보낸 데이터는 수정하면 안됨 

```jsx
예를들어
<h4 @click="모달창열렸니 = true">{{원룸.title}}</h4>
이런식으로 모달창열렸니 라는 props를 수정하면 오류발생함
```

- 여러곳에서 데이터를 사용하게되면 자식이 아닌 최고 최상위 부모컴포넌트에 만들어주는게 좋음

```jsx
<Modal :데이터이름 = "데이터이름"/>
-> 이런식으로 데이터를 바인딩해서 보내줘야함

[app.vue]

<Modal :원룸들 = "원룸들"/>

[Modal.vue]

<template>
  <!-- 모달창 관련 코드 생략 -->
</template>

<script>
export default {
    name : 'Modal',
		props : {
        원룸들 : Array,
    }
		-> 자식은 props 받은거 등록
    -> props : {데이터이름: 자료형이름},
}
</script>

<style>

</style>
```

> 자식이 부모데이터를 바꾸고 싶으면 custom event로 메세지를 보내야함
> 
- 부모에게 메세지 보낼땐 $emit(’작명’, 데이터)
- 부모가 메세지 수신할땐 @작명한거= “”
- 자식이 보낸 데이터는 $event 변수에 담겨있음

```jsx
[자식]
<template>
   <div>
     <img :src="원룸.image" class="room-img">
     <h4 @click="$emit('openModal')">{{원룸.title}}</h4>
     <p>{{원룸.price}}원</p>
   </div>
</template>

[부모]
<template>
	<Card @openModal="true; 누른거 = $event;" :원룸="원룸들[i]" 
	v-for="(a,i) in 원룸들" :key="a"/>
</template>
```

- $emit()을 함수안에 하고싶으면 this.$emit()

```jsx
<template>
	<h4 @click="함수">{{원룸.title}}</h4>
</template>

<script>
	methods : {
		함수(){
			this.$emit('openModal', this.원룸.id)
			}
		}
</script>
```

### Input

- input에 사용자가 입력한 값을 사용할때 사용됨

```jsx
<input @input="month = event.target.value">
->event.target.value 이게 input에 입력한 값과 동일함

<input v-model="month">
-> 위에꺼와 동일! v-model="여기"
-> 여기 들어오는 값을 month 에 저장

자바스크립트에서 더하기 연산의 경우 문자처럼 옆으로 붙음
EX) 123 + 456 = 123456
이걸 방지하고 연산하려면 v-model.number="month" 
```

### Watcher로 Input 내용 감시하기

- Data를 감시하는 함수
- 데이터가 변할때마다 watch에 있는 코드가 실행됨

```jsx
watch : {
      month(a){
        if(a>12){
          alert("13 이상의 값은 입력할 수 없습니다.");
        }
      }
    },
```

### CSS로 애니메이션 주기

1. 시작전 class명
2. 애니메이션 끝난 후 class명
3. 그리고 원할 때 2번 class명 부착

- class명을 조건부로 넣으려면 {class명 : 조건}
- Vue에서는 특별한 위와 동일한 기능제공 TRANSITION
1. 애니메이션 주고싶은 요소를 감싸기
2. class명 3개 작성

<aside>
👉 .fade-enter-from{}
.fade-enter-active{}
.fade-enter-to{}

</aside>

```jsx
[일반적인 CSS]
<div class="start" :class="{end : true}">
    <Modal :원룸들 = "원룸들" :누른거 = "누른거" 
		:모달창열렸니 = "모달창열렸니" @closeModal = "모달창열렸니 = false;"/>
</div>

[VUE]
<transition>
    <Modal :원룸들 = "원룸들" :누른거 = "누른거" 
		:모달창열렸니 = "모달창열렸니" @closeModal = "모달창열렸니 = false;"/>
</transition>
```

- Array/Object 데이터의 각각 별개의 사본을 만들려면 [...array자료] 이렇게 만들어야함
