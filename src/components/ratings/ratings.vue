<template>
  <div class="ratings">
    <div class="ratings-content">
      <div class="overview">
        <div class="overview-left">
          <h1 class="score">{{seller.score}}</h1>
          <div class="title">综合评分</div>
          <div class="rank">高于周边商家{{seller.rankRate}}%</div>
        </div>
        <div class="overview-right">
          <div class="score-wrapper">
            <span class="title">服务态度</span>
            <star :size="36" :score="seller.serviceScore"></star>
            <span class="score">{{seller.serviceScore}}</span>
          </div>
          <div class="score-wrapper">
            <span class="title">商品评分</span>
            <star :size="36" :score="seller.foodScore"></star>
            <span class="score">{{seller.foodScore}}</span>
          </div>
          <div class="delivery-wrapper">
            <span class="title">送达时间</span>
            <span class="delivery">{{seller.deliveryTime}}分钟</span>
          </div>
        </div>
      </div>
      <split></split>
      <ratingselect :selectType="selectType" :onlyCotent="onlyContent"></ratingselect>
    </div>
  </div>
</template>
<script>
import star from '../star/star'
import split from '../split/split'
import ratingselect from '../ratingselect/ratingselect'

const ERR_OK = 0;
const ALL = 2;

export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      ratings: [],
      selectType: ALL,
      onlyContent: false,
    }
  },
  created() {
    this.$http.get('api/ratings').then(response => {
      if (response.body.errno === ERR_OK)
        this.ratings = response.body.data;
    console.log(this.ratings);
    })
  },
  components: {
    star,
    split,
    ratingselect
  }
};
</script>
<style lang="stylus" scoped>
  .ratings
    position: absolute
    top: 174px
    bottom: 0
    left: 0
    width: 100%
    overflow: hidden
    .overview
      display: flex
      padding: 18px 0
      .overview-left
        padding: 6px 0
        flex: 0 0 137px
        width: 137px
        border-right: 1px solid rgba(7,17,27,0.1)
        text-align: center
        @media only screen and (max-width:320px)
          flex: 0 0 120px
          width: 120px
        .score
          margin-bottom: 6px
          line-height: 28px
          font-size: 24px
          color: rgb(255,153,0)
        .title
          margin-bottom: 8px
          line-height: 12px
          font-size: 12px
          color: rgb(147,153,159)
        .rank
          line-height: 10px
          font-size: 10px
          color: rgb(147,153,159)
      .overview-right
        flex: 1
        padding: 6px 0 6px 24px
        @media only screen and (max-width: 320px)
          padding-left: 6px
        .score-wrapper
          margin-bottom: 8px
          font-size: 0
          .title
            display: inline-block
            line-height: 18px
            vertical-align: top
            font-size: 12px
            color: rgb(7,17,27)
          .star
            display: inline-block
            vertical-align: top
            margin: 0 12px
          .score
            display: inline-block
            line-height: 18px
            vertical-align: top
            font-size: 12px
            color: rgb(255,153,0)
        .delivery-wrapper
          font-size: 0
          .title
            line-height: 18px
            font-size: 12px
            color: rgb(7,17,27)
          .delivery
            margin: 12px
            font-size: 12px
            color: rgb(147,153,159)

</style>
