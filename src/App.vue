<template>
  <!-- 
    Props
    용어 정리 : 부모/ 자식 컴포넌트
    App.vue => 부모
    Modal.vue => 자식
    자식 컴포넌트가 부모 컴포넌트의 데이터를 쓰려면
    props로 데이터를 전송해야함.

    props의 3 step!
    1. 데이터 보내고
    2. 등록하고
    3. 쓰자.

    1. v-bind or : 
    <자식 :데이터="데이터">

     !!주의
    props는 read-only임.
    수정하면 큰일남.
  -->
  
  <MyModal :products="products" :pushData="pushData" :모달창상태="모달창상태"  @closeModal="모달창상태 = false;"/>

  <!-- HTML반복문 
    <태그 v-for="작명 in 몇회" :key="작명"> 키가 반드시 필요함.
    몇회에 자료형을 집어 넣으면 자료형 랭스 만큼 돈다.
    key는 반복문 돌린 요소를 컴퓨터가 구부나기 위해 씀.

    메뉴는 어레이 내 각 데이터가 꼿힐 곳. i는 반복 인덱스

  -->
  
  <div class="menu">
    <a v-for="(메뉴,i) in 메뉴들" :key="i">{{ 메뉴 }}</a>
    <!-- <h1 v-for="메롱 in 3" :key="메롱">메롱</h1> -->
  </div>

  <!--컴포넌트화 하기
    1. vue 파일 생성 < 엔터하면 바로 나옴
    2. 축약할 html 넣기
    3. 익스포트 디폴트에 name속성 넣기

    사용 방법
    1. vue 파일 import
    2. 컴포넌트에 등록
    3. 사용

    사용 이유
    - 아름답다. 
    - 재사용이 쉽다.
    - 모든 걸 다 컴포넌트 하지마노 반복적으로 출현할 부분만 컴포넌트화 하자.
    - 데이터 바인딩이 귀찮아 질 수있다.
    - 왜냐면 데이터 바인딩은 같은 파일에 있는 것들만 가능하기 때문
    - 보통은 App.vue에 데이터 다 밀어넣고 여기껄 가져다 씀. props

    !주의
    자식 컴포넌트에서만 쓸 데이터라면 자식 컴포넌트에 데이터를 만들어도 되지만
    부모도 쓰는 데이터라면 부모 컴포넌트에 만들어라.

    보통 같은 데이터를 사용하는 최상의 부모에서 만드는 것이 일반적이다


   
  -->
  <myDiscount/>
 
  
  <!--컴포넌트화 하기-->


  <!--이미지 경로 보통 assets 폴더에 넣음.
      절대 경로는 그냥 다쓰면 되고
      상대경로는 src에 있는 거 가져올때 ./ 또는 ..

      이벤트 버블링으로 컴포넌트에 
      @click="모달창열렸니 = true" 걸어도 되긴함.

      커스텀 이벤트

      emit으로 보낸거 받을땐, @작명이름
      자식이 openModal 이름의 메세지를 보내면 자바스크립트 실행해주셈~ 이라는 뜻
      자식이 보낸 메세지의 데이터를 꺼내려면 $event를 쓰면된다.
  -->
  
  <MyCard v-for="(product,i) in products" :key="i" :product="product" 그냥="도보낼수있다"  :숫자로="123"
  @openModal="모달창상태= true; pushData = $event" 
  />
  <!-- 데이터 입니다 ================================================================= -->
  <!-- 속성 데이터 바인딩 :어쩌구 내용 데이터바인딩 {{ 어쩌구 }}-->
  <!-- <div v-for="(product,i) in products" :key="i"> -->
    <!-- <img :src="require(`@/assets/room${i}.jpg`)" class="room-img"> -->
    <!-- <img :src="products[i].image" class="room-img"> -->
    <!-- <h4 @click="modalopen(products[i].id)" class="red" :style="스타일">{{  products[i].title }}</h4> -->
    <!-- <p>{{  products[i].price }}원</p> -->
    <!-- <button @click="increase(i,$event)">허위매물신고</button>   -->
    <!-- v-on: 또는 @ 
        이벤트 종류
        click, mouseover, drag..
    -->
    <!-- <span>신고수 : {{ 신고수[i] }}</span> -->
  <!-- </div> -->
  <!-- 데이터 입니다 ================================================================= -->
</template>

<script>
// default 안쓰면 중괄호로 묶어야함.
// import {apple, apple2} from './assets/oneroom.js';
import onerooms from './assets/oneroom.js';
import myDiscount from './Discount.vue';
import MyModal from './Modal.vue';
import MyCard from './Card.vue';
/*
  자바스크립트에서 함수 쓰는 이유
  긴 코드를 짧은 단어하나로 축약할 수 있는 것이 함수이다.

*/

export default {
  name: 'App',
  data(){
    // 뷰 개발 꿀팁 은 데이터를 어떻게 만들지 부터 생각하는것이 매우 좋음.
    return {
      /*
      데이터 바인딩 하는 이유
      1. 가변 데이터들 
      2. [핵심] Vue의 실시간 자동 렌더링 쓰려면 해야됨.
      data를 변경하면 data와 관련된 HTML에도 실시간으로 반영됨. 
      값 바인딩 {{ 데이터명 }}
      속성 바인딩 :속성 = "데이터명"
      */
      // price1 : 60,
      // price2 : 70,
      // price3 : 80,
      스타일 : 'color :blue',
      prices : [60,70,80],
      products : onerooms,
      메뉴들 : ['Home', 'Shop', 'About'],
      신고수 : [0,0,0,0,0,0],
      모달창상태 : false, // false은 닫힘 true은 열림
      pushData :0,
    }
  },
  // 함수는 데이터 뒤에 methods 써서 함수공간 만드셈 글고 함수(){} 이렇게 하면됨
  methods:{
    increase(i){
      // 큰 오브젝트를 가르키고 있어야 먹음. 함수안에 지역변수가 없기때문에 안뜨는 거임.
      this.신고수[i] += 1;
    },
    modalopen(i){
      if(this.모달창상태 == true){
        this.모달창상태 = false;
      }else{
        this.모달창상태 = true;
        this.pushData = i;
      }
      
    }
  },
  components: {
    myDiscount : myDiscount,
    MyModal : MyModal,
    MyCard : MyCard,
  }
}
</script>
<!--
  동적인 UI 만드는 법
  0. HTML, CSS 디자인 해둠
  1. UI의 현재 상태를 데이터로 저장해둠.
  2. 데이터에 따라 UI가 어떻게 보일지 작성
-->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

.menu {
  background : darkslateblue;
  padding : 15px;
  border-radius : 5px;
}
.menu a {
  color : white;
  padding : 10px;
}

.room-img{
  width : 100%;
  margin-top : 40px;
}

body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
} 
.discount{
  background: #eee;
  padding :10px;
  margin: 10px;
  border-radius : 5px;
}
</style>
