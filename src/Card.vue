<template>
  <!-- 데이터 입니다 ================================================================= -->
  <!-- 속성 데이터 바인딩 :어쩌구 내용 데이터바인딩 {{ 어쩌구 }}
        부모 데이터가 변경하고 싶다면 직접변경하는 것이 아닌 부모에게 사실을 알려라.
        부모에게 알리기 $emit('작명', 데이터)

        $어쩌구 는 Vue의 내장된 특별한 변수
-->
  <div>
    <!-- <img :src="require(`@/assets/room${i}.jpg`)" class="room-img"> -->
    <img :src="product.image" class="room-img">
    <!-- <h4 @click="modalopen(products[i].id)" class="red" :style="스타일">{{  products[i].title }}</h4> -->
    <h4 @click="send" class="red" :style="스타일">{{  product.title }}</h4>
    <p>{{  product.price }}원</p>
    <!-- <button @click="increase(i,$event)">허위매물신고</button>   -->
    <!-- v-on: 또는 @ 
        이벤트 종류
        click, mouseover, drag..
    -->
    <span>신고수 : {{ product.신고수 }}</span>
  </div>
  <!-- 데이터 입니다 ================================================================= -->
</template>

<script>
export default {
    name: 'MyCard',
    props :{
        product : Object,
    } ,
    methods :{
        send(){
            this.$emit('openModal', this.product.id);
        }
        
    }
}
</script>

<style>

</style>