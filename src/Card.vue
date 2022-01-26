<template>
   <div v-for="(a,i) in 원룸들" :key="i">
     <img :src="원룸들[i].image" class="room-img">
     <h4>{{원룸들[i].title}}</h4>
     <p>{{원룸들[i].price}}원</p>
   </div>
</template>

<script>
export default {
 name : 'Card',
 props : {
     원룸들 : Array,
 }
}
</script>

<style>

</style>