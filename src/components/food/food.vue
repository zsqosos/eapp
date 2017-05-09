<template>
  <transition name="move">
    <div v-show="foodShow" class="food" ref="food">
      <div class="food-content">
        <div class="image-wrapper">
          <img class="img" :src="food.image">
          <div class="back" @click="back">
            <i class="icon-arrow_lift"></i>
          </div>
        </div>
        <div class="content">
          <h1 class="title">{{food.name}}</h1>
          <div class="detail">
            <span class="sell-count">月售{{food.sellCount}}份</span>
            <span class="rating">好评率{{food.rating}}</span>
          </div>
          <div class="price">
            ￥
            <span class="now">{{food.price}}</span>
            <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
          </div>
          <transition name="buyFade">
            <div class="buy" v-show="!food.count || food.count===0" @click.stop.prevent="addFirst">加入购物车</div>
          </transition>
          <div class="cartcontrol-wrapper">
            <cartcontrol :food="food"></cartcontrol>
          </div>
        </div>
        <split v-show="food.info"></split>
        <div class="info" v-show="food.info">
          <h1 class="title">商品信息</h1>
          <p class="text">{{food.info}}</p>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import iscroll from 'iscroll'
import cartcontrol from '../cartcontrol/cartcontrol'
import split from '../split/split'

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
      this.$nextTick(function () {
        if (!this.scroll) {
          this.scroll = new iscroll(this.$refs.food);
        }
        this.scroll.refresh();
      });
    },
    back() {
      this.foodShow = false;
    },
    addFirst() {
      if (!this.food.count) {
        this.$set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
      this.$root.$emit('add_cart', event.target);
    }
  },
  components: {
    cartcontrol,
    split
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
      .content
        position: relative
        padding: 18px
        .title
          margin-bottom: 8px
          line-height: 14px
          font-size: 14px
          font-weight: 700
          color: rgb(7,17,27)
        .detail
          margin-bottom: 18px
          height: 10px
          line-height: 10px
          font-size: 0
          .sell-count,.rating
            font-size: 10px
            color: rgb(147,153,159)
          .sell-count
            margin-right: 12px
        .price
          line-height: 24px
          font-size: 10px
          font-weight: 700
          color: rgb(240,20,20)
          .now
            margin-right: 8px
            font-size: 14px
          .old
            text-decoration: line-through
            color: rgb(147,153,159)
        .cartcontrol-wrapper
          position: absolute
          right: 12px
          bottom: 12px
        .buy
          position: absolute
          right: 18px
          bottom: 18px
          padding: 0 12px
          z-index: 10
          height: 24px
          line-height: 24px
          border-radius: 12px
          font-size: 10px
          color: #fff
          background: rgb(0,160,220)
          transition: all 0.2s
          &.buyFade-leave-active,&.buyFade-enter
            opacity: 0
      .info
        padding: 18px
        .title
          line-height: 14px
          margin-bottom: 6px
          font-size: 14px
          color: rgb(7,17,27,)
        .text
          line-height: 24px
          padding: 0 8px
          font-size: 12px
          color: rgb(77,85,93)
</style>
