<template>
    <div class="star" :class="starType">
      <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" v-bind:key="index">{{index}}</span>
      <!-- <span v-for="testItems in testItem" :class="testItems" class="star-item">{{testItems}}</span> -->
    </div>
</template>

<script>
const LENGTH = 5;
const CLS_ON = "on";
const CLS_HALF = "half";
const CLS_OFF = "off";
export default {
  props: ["size", "score"],
  computed: {
    starType() {
      return "star-" + this.size;
    },
    itemClasses() {
      console.log(123);
      
      let result = [];
      let score = Math.floor(this.score * 2) / 2;
      let hasDecimal = score % 1 !== 0;
      let integer = Math.floor(score);
      for (let i = 0; i < integer; i++) {
        result.push(CLS_ON);
      }
      if (hasDecimal) {
        result.push(CLS_HALF);
      }
      while (result.length < LENGTH) {
        result.push(CLS_OFF);
      }
      return result
    },
    testItem() {
      return ["1", "2", "3"];
    }
  }
};
</script>
<style scoped>
.star .star-item {
  display: inline-block;
  background-repeat: no-repeat;
}
.star.star-48 .star-item {
  width: 20px;
  height: 20px;
  margin-right: 22px;
  background-size: 20px 20px;
}
</style>
