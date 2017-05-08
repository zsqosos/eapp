<template>
  <transition name="move">
    <div v-show="foodShow" class="food">
      <div class="food-content">
        <div class="image-wrapper">
          <img class="img" :src="food.image">
          <div class="back" @click="back">
            <i class="icon-arrow_lift"></i>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  data() {
    return {
      foodShow: false
    }
  },
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    show() {
      this.foodShow = true;
    },
    back() {
      this.foodShow = false;
    }
  }
};
</script>

<style lang="stylus">
  .food
    position: fixed
    top: 0
    left: 0
    bottom: 48px
    z-index: 30
    width: 100%
    background: #fff
    transition: all 0.5s
    &.move-enter,&.move-leave-active
      transform: translate3d(100%,0,0)
    .food-content
      .image-wrapper
        position: relative
        width: 100%
        height: 0
        padding-top: 100%
        .img
          position: absolute
          top: 0
          left: 0
          width: 100%
          height: 100%
        .back
          position: absolute
          top: 10px
          left: 0
          .icon-arrow_lift
            display: block
            padding: 10px
            font-size: 20px
            color: #fff
</style>
