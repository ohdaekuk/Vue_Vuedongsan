<template>

<!--모달창-->
<transition name="fade">
  <Modal @closeModal="모달 = false;" :원룸들="원룸들" :제목클릭="제목클릭" :모달="모달" />
</transition>

<!-- 메뉴 -->
  <div class="menu">
    <a v-for="(a, i) in 메뉴" :key="i">{{a}}</a>
  </div>

<!-- 배너 -->
<transition name="show">
  <Discount v-if="show == true" :할인="할인"/>
</transition>

  <button @click="priceSortLow">가격낮은순정렬</button><br><br>
  <button @click="priceSortHigh">가격높은순정렬</button><br><br>
  <button @click="sortBack">되돌리기</button>

<!-- 본문 -->
  <Card @openModal="모달 = ture; 제목클릭 = i" :원룸들="원룸들[i]" :모달="모달" v-for="(a, i) in 원룸들" :key="a" />

</template>

<script>

import room from './data.js';
import Discount from './Discount.vue'
import Modal from './Modal.vue'
import Card from './Card.vue'


export default {
  name: 'App',

  data(){
    return {
      원룸들오리지널 : [...room],
      메뉴 : ['Home', 'Product', 'About'],
      신고수 : [0, 0, 0, 0, 0, 0],
      모달 : false,
      원룸들 : room,
      제목클릭 : 0,
      show : true,
      할인 : 30
    }
  }, 

  methods :{
    increase(a){
      this.신고수[a] += 1;
    },
    priceSortLow(){
      this.원룸들.sort(function(a, b){
        return a.price-b.price
      })
    },
    priceSortHigh(){
      this.원룸들.sort(function(a, b){
        return b.price-a.price
      })
    },
    sortBack(){
      return this.원룸들 = [...this.원룸들오리지널]
    },
  },

  mounted(){
    setInterval(() => {
      this.할인--;  
      if(this.할인 < 1){
        this.할인 = 0
      }
    }, 1000);
  },

  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card
  }
}
</script>

<style>
/* modal에 애니메이션 주기 */
.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to{
  opacity: 0;
}

.fade-enter-from {
  transform: translateX(-300px);
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to{
  opacity: 1;
}

/* ============================== */

.show-leave-from {
  opacity: 1;
}

.show-leave-active {
  transition: all 1s;
}

.show-leave-to{
  opacity: 0;
}

body{
  margin: 0;
}

div{
  box-sizing: border-box;
  }

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a{
  color: white;
  padding: 10px;
}

.room-img{
  width: 70%;
  margin-top: 30px;
}

.black-bg{
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0, 5);
  position: fixed; padding: 20px;
  
}

.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
  border: 1px black solid;
}

.modal_image{
  width: 70%; height: 70%;
  margin: 0 auto;
  padding: 10px;
}

.modal_h4{
  width: 30%;
  margin: 0 auto;
}
</style>