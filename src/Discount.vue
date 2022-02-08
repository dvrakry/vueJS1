<template>
    <!-- 할인배너 -->
  <div class="discount" v-if="discount == true">
    <h4>지금 결제하면 {{percent}}% 할인</h4>
  </div>
</template>

<script>
export default {
    name : 'Discount',
    data(){
      return{
        percent : 5,
        discount: true,
      }
    },

    mounted(){
      setInterval(() => {
        if(this.percent > 0){
          this.percent--; 
        } else if(this.percent < 1){
          this.showDiscount = false
        }
    }, 1000);

    }
    
}
</script>

<style>

</style>