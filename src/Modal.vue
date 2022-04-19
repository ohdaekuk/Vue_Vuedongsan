<template>
  <div class="black-bg" v-if="모달 == ture">
    <div class="white-bg">
      <img class="modal_image" :src="원룸들[제목클릭].image">
      <h4>{{원룸들[제목클릭].title}}</h4>
      <p>{{원룸들[제목클릭].content}}</p>
      <!-- <input @input="month = $event.target.value" type="text"> -->
      <input v-model="month"> 
      <!-- v-model => input, textarea, select 등의 값을 data에 저장한다 -->
      <p>{{month}}개월 선택함 : {{원룸들[제목클릭].price * month}}원</p>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data(){
    return{
      month : 0
    }
  },
  // watch :{
  //   // month(i, z){   
  //   //   if(i > 12){
  //   //     alert("13개월 이상은 ㄴㄴ");
  //   //     this.month = z;
  //   //   }
  //   // }
  // //   month(i){
  // //     if(isNaN(i) == true){
  // //       alert("숫자만 가능합니다");
  // //       this.month = 1;
  // //     }
  // //   }
  // // },
  beforeUpdate(){

    if(isNaN(this.month) == true){
      alert("숫자만 가능합니다.")
      this.month = 1;
    }

    if(this.month == 2 || this.month == 1){
      alert("2개월 이상 계약 가능합니다");
      this.month = 3;
    }
  },
  props : {
    원룸들 : Object,
    제목클릭 : Number,
    모달 : Boolean
  }
}
</script>

<style>

</style>