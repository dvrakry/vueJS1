<template>
  
  <Modal :원룸들 = "원룸들" :누른거 = "누른거" :모달창열렸니 = "모달창열렸니" @closeModal = "모달창열렸니 = false;"/>

  <div class="menu">
    <a v-for="작명 in 메뉴들" :key="작명">{{작명}}</a>
  </div>

  <Discount/>

  <Card @openModal="모달창열렸니=true; 누른거 = $event" :원룸="원룸들[i]" v-for="(a,i) in 원룸들" :key="a"/>
  <!-- <Card  :원룸="원룸들[1]"/>
  <Card  :원룸="원룸들[2]"/>
  <Card  :원룸="원룸들[3]"/>
  <Card  :원룸="원룸들[4]"/>
  <Card  :원룸="원룸들[5]"/> -->

   <!-- <div v-for="(a,i) in 원룸들" :key="i">
    <img :src="원룸들[i].image" class="room-img">
    <h4 @click="모달창열렸니 = true; 누른거 = i">{{원룸들[i].title}}</h4>
    <p>{{원룸들[i].price}}원</p>
  </div> -->
  
  
  <!-- 원룸들[i] = a -->


  <!-- <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{products[1]}}</h4>
    <p>60 만원</p>
    <button @click="신고수[1]++">허위매물신고</button> 
    <span>신고수 : {{신고수[1]}}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}}</h4>
    <p>65 만원</p>
    <button @click="신고수[2]++">허위매물신고</button> 
    <span>신고수 : {{신고수[2]}}</span>
  </div> -->

</template>

<script>

import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';


export default {
  name: 'App',
  data(){
    return {
      누른거 : 0,
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0,0,0],
      메뉴들 : ['Home', 'Shop', 'AbouT'],
      products : ['신설동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase(){
      this.신고수 += 1
    }
  },
  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding : 10px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}

.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
