<template>
  <!--모달창 만들어 보기======================================================-->
  <!-- v-if는 v-if="조건식" 조건식이 참일 때 보임-->
  <div v-if="1==2">
    안녕하세요
  </div>
  <div v-else-if="1==3">
    안녕하세요2
  </div>
  <!-- v 문법에서만 "" 안에서 데이터이름을 바로 써줘도 인지를 한다-->
  <div class="black-bg" v-if="모달창상태 == true">
    <div class="white-bg">
      
      <img :src="products[pushData].image" style="width:100%">
      <h4>{{products[pushData].title}}</h4>
      <p>{{products[pushData].content}}</p>
      <!-- @input 인풋이벤트 >> 입력할때마다 실행해주셈
        이벤트 리스너 $event  == e 와 같은 역할
        HTML요소.addEventListener('click', function(e){
            e.target (내가 클릭한 요소를 뜻함.)
            e.preventDefault (기본동작막기)
                    })

        
        축약버전 v-model == @input="month =$event.target.value"
        input류의 모든 태그에 붙일 수 있음. select, textarea,checkbox...
        v-model 은 여기에 입력한 데이터를 밑에 데이터에 저장해주세요 라는 뜻
        v-model="사용자가 입력한 데이터를 저장할 데이터 공간(state에 있는 데이터)"
        
        vue에서는 콘솔로그 못한다~~ 알고 있거라~~ 
    -->
      <!-- <input @input="month =$event.target.value">
        v-model.number 이러면 타입지정도 가능함.
    -->
      <input v-model="month">
      <p>{{ month }}개월 선택함 : {{products[pushData].price * month}}원</p>
    </div>
    <button @click="$emit('closeModal')">닫기</button>
  </div>
  <!--모달창 만들어 보기======================================================-->
</template>

<script>
export default {
    name: 'MyModal',
    data(){
        return{
            month : 1,
        }
    },
     // 감시 !
  watch:{
    //데이터 이름과 동일하게 하면 그 데이터를 감시함.
      month(input){
        // isNaN = Not a Number >> isNaN(input)
        if(isNaN(input)){
            this.month =1;
            alert('숫자만 입력해줘요!')
        }else{
            if(input > 13 ) {
                alert('13이상 입력 금지')
                this.month = 1;
            }
        }
   
      
      
     
      
        
      
    },
  },
    props :{
        // props 데이터 보낸 이름 : 자료형
        products : Array,
        pushData : Number,
        모달창상태 : Boolean,
    },
    methods:{
        함수(){

        }
    }
}
</script>

<style>

</style>