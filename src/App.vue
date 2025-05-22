<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <p :style="스타일">{{ price }}쀼</p>

  <button @click="모달창열렸니 = true">모달열림</button>

  <DiscountComponent v-if="showDiscount == true" :count="count"/>

  <button @click="priceLowSort">가격낮은순정렬</button>
  <button @click="priceHighSort">가격높은순정렬</button>
  <button @click="ABCSort">가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <!-- <div class="start" :class="{end : 모달창열렸니}">   </div>-->
  <transition name="fade">
    <ModalComponent
      :post="post"
      :모달창열렸니="모달창열렸니"
      :누른거인덱스="누른거"
      :제목="제목"
      @closeModal="모달창열렸니 = false"
    />
  </transition>

  <RoomCard
    @hypeBoy="
      모달창열렸니 = true;
      누른거 = $event;
    "
    @hypeGirl="
      제목 =  $event;
    "
    v-for="(a, i) in post"
    :key="i"
    :onePost="post[i]"
  />
</template>

<script>
import DiscountComponent from "./DiscountComponent.vue";
import post from "./post";
import ModalComponent from "./ModalComponent.vue";
import RoomCard from "./RoomCard.vue";

export default {
  name: "App",
  data() {
    return {//왼쪽은 작명, 오른쪽엔 데이터를 넣는다.
      count:50,
      showDiscount: true,
      postOriginal: [...post],

      제목:"",

      누른거: 0,
      post: post,
      모달창열렸니: false,
      이미지: [
        "https://img.stibee.com/16255_1628237873.jpg",
        "https://i.ytimg.com/vi/5tTN4DxI4b4/hqdefault.jpg",
        "https://i.ytimg.com/vi/j5BNLexikF0/hq720_2.jpg?sqp=-oaymwEYCI4CEOADSFryq4qpAwo" +
          "IARUAAIhC0AEB&rs=AOn4CLAzXsDsQe0MCLIGw44NDlRML_N9gQ",
      ],
      좋아요: [0, 0, 0],
      스타일: "color:red",
      메뉴들: ["Home", "Shop", "About"],
      products: ["임대범", "김대범", "박대범"],
      가격: [60, 70, 80],
    };
  },
  methods: {
    increase(i) {
      this.좋아요[i]++;
    },
    priceLowSort() {
      this.post.sort(function (a, b) {
        return a.price - b.price;
      });
    },
    priceHighSort() {
      this.post.sort(function (a, b) {
        return b.price - a.price;
      });
    },
    ABCSort() {},
    sortBack() {
      this.post = [...this.postOriginal];
    },
  },
  mounted() {
    const intervalId = setInterval(() => {
      if (this.count > 0) {
        this.count--;
      } else {
        clearInterval(intervalId);
      }
    }, 1000); 
  },

  components: {
    DiscountComponent,
    ModalComponent,
    RoomCard,
  },
};
</script>

<style>
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

.start {
  opacity: 0;
  transition: all 1s;
}

.end {
  opacity: 1;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
.menu {
  background: white;
  padding: 10px;
  border-radius: 5px;
}
.box {
  border: 2px solid #000;
  z-index: 1;
  /* 기본적으로는 1로 설정합니다. */
}

.box2 {
  border: 2px solid #000;
  z-index: 2;
  width: 50%;
  height: 50%;
  background: aliceblue;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px;
  box-sizing: border-box; /* 컨텐츠가 패딩과 경계선을 포함하도록 설정 */
}
.menu {
  color: white;
  padding: 10px;
}

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 50%;
  height: 50%;
  background: #2c3e50;
  position: fixed;
  padding: 20px;
}

.white-bg {
  width: 50%;
  background: white;
  border-radius: 8px;
  position: fixed;
  padding: 20px;
}
</style>
