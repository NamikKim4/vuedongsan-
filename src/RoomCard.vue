<template>
  <div class="box">
    <h4>{{모달창열렸니}}😶</h4>
    <img :src="onePost.image" @click="$emit('hypeBoy', onePost.id)" />

    <h4 @click="newJeans">
      {{ onePost.title }}
    </h4>    

    <p>{{ onePost.price }}만원</p>
    <p>{{ onePost.content }}만원</p>
  </div>
</template>

<script>
export default {
  name: "RoomCard",
  props: { //부모에서 받아온 props🌲🌲🌲
    모달창열렸니:Boolean,
    onePost: Object,
    누른거:Object
  },
  methods : {
    newJeans(){
      this.$emit('hypeGirl', this.onePost.title)
    }
  }
};
</script>

<style></style>
