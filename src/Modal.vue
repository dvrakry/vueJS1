<template>
  <!-- 모달창 -->
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image">
      <h4>{{원룸들[누른거].title}}</h4>
      <p>{{원룸들[누른거].content}}</p>
      <!-- <input @input="month = $event.target.value"> -->
      <input v-model="month">
      <p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}} 원 </p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>

</template>

<script>
export default {
    name : 'Modal',
    data(){
      return {
        month : 1,
      }
    },
    watch : {
      month(a){
        if(a>12){
          alert("13 이상의 값은 입력할 수 없습니다.");
        } else if(isNaN(a) == true){
          alert("숫자만 입력해주세요");
          this.month = 1;
        }
      },
    },
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
        
    },

    updated(){
      if(this.month == 2){
        alert("2 입력됨")
      }
    }
}
</script>

<style>

</style>