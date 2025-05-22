<template>

    <div class="box2" v-if="모달창열렸니 == true">
    <h4>{{제목}}🐰🐰🐰</h4>
        {{누른거인덱스}}🌲🌲🌲
    <h4>{{post[누른거인덱스].title}}</h4>
    <p>{{post[누른거인덱스].content}}</p>
    <p>월세 : {{post[누른거인덱스].price}} 원</p>
    개월수 입력 : <input @input="month = $event.target.value"><br/>
    <p>{{month}}개월 선택함  👉  {{post[누른거인덱스].price * month}}원 입니다.</p>
   
    <!-- <input v-model.number="day"> -->
    <!-- <p>{{day}}일</p> -->

    <button @click="$emit('closeModal')">닫기</button>
    </div>
</template>

<script>
export default {
name:'ModalComponent',
data(){ //데이터의 초기값을 정의
    return{
        month : 1,
        day:8
    }
},
 watch: {
    month(a) {
      if (isNaN(a)) {
        alert("숫자만 입력하세요.");
        this.month = 1; // 또는 ''로 초기화할 수도 있어요
        return;
      }
      if (a >= 13) {
        alert("12 이하로 입력하세요.");
      }
    }
  },
props: {
    post: Array,
    누른거인덱스:Number,
    모달창열렸니:Boolean,
    제목:String
  },
}
</script>

<style>

</style>