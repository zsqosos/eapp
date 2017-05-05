<template>
  <div class="cartcontrol">
    <div v-show="food.count>0" class="decrease icon-remove_circle_outline" @click="decreaseCart"></div>
    <div v-show="food.count>0" class="count">{{food.count}}</div>
    <div class="add icon-add_circle" @click="addCart"></div>
  </div>
</template>
<script>
import Vue from 'Vue';
export default {
  props: {
    food: {
      type: Object,
    }
  },
  data() {
    return {
    };
  },
  methods: {
    addCart(event) {
      if (!event._constructed) {
        return;
      }
      if (!this.food.count) {
        // this.food.count = 1;
        this.$set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
      console.log(this.food.count);
    },
    decreaseCart(event) {
      if (!event._constructed) {
        return;
      }
      if (this.food.count) {
        this.food.count--;
      }
      console.log(this.food.count);
    }
  }
}
</script>
<style lang="stylus" scoped>
  .cartcontrol
    font-size: 0
    .decrease,.add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
    .count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147,153,159)
</style>
