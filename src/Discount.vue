<template>
  <div class="discount">
    <h4>지금 결제하면 {{할인}}% 할인</h4>
  </div>
</template>

<script>
export default {
  name: 'Discount',
  props:{
    할인 : Number
  }
  // data(){
  //   return{
  //     할인 : 20

  //   }
  // }
}
</script>

<style>
  .discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>