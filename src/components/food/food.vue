<template>
  <div class="food" v-show="showFlag" transition="move" v-el:food>
    <div class="food-content">
      <div class="image-header">
          <img :src="food.image">
          <div class="back" @click="hide">
            <i class="icon-arrow_lift"></i>
          </div>
      </div>
      <div class="content">
        <h1 class="title">{{food.name}}</h1>
        <div class="food-detail">
          <span class="sell-count">月售{{food.sellCount}}份</span><span class="rating">好评率{{food.rating}}%</span>
        </div>
        <div class="price">
            <span class="now">￥{{food.price}}</span>
            <span class="old" v-show="food.oldPrice">￥{{food.oldPrice}}</span>
        </div>
        <div class="cartcontrol-wrapper">
          <cartcontrol :food="food"></cartcontrol>
        </div>
        <div class="buy" v-show="!food.count || food.count === 0" @click.stop.prevent="addFirst($event)" transition="fade">
            加入购物车
        </div>
      </div>
      <split v-show="food.info"></split>
      <div class="info" v-show="food.info">
        <div class="title">商品介绍</div>
        <p class="text">{{food.info}}</p>
      </div>
      <split v-show="food.ratings"></split>
      <div class="rating">
        <h1 class="title">商品评价</h1>
        <ratingselect></ratingselect>
      </div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue';
  import BScroll from 'better-scroll';
  import cartcontrol from 'components/cartcontrol/cartcontrol';
  import split from 'components/split/split';
  import ratingselect from 'components/ratingselect/ratingselect';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    data: ()=>({
      showFlag: false
    }),
    methods: {
      show() {
        this.showFlag = true;
      },
      hide() {
        this.showFlag = false;
      },
      addFirst(event) {
        if(!event._constructed) {
          return;
        }
        // 动画效果
        // this.$dispatch('cart.add',event.target);
        Vue.set(this.food, 'count', 1);
      }
    },
    components: {
      cartcontrol,
      split,
      ratingselect
    }
  };
</script>

<style lang="stylus">
  .food
    position: fixed
    left: 0
    bottom: 48px
    z-index: 30
    width: 100%
    height: 100%
    background: #fff
    &.move-transition
      transition: all 0.4s linear
      transform: translate3D(0,0,0)
    &.move-enter, &.move-leave
      transform: translate3D(100%,0,0)
    .image-header
      position: relative
      width: 100%
      height: 0
      /*黑魔法 设置一个宽高相等的盒子*/
      padding-top: 100%
      img
        position: absolute
        top: 0
        left: 0
        width: 100%
        height: 100%
    .back
        position: absolute
        top: 60px
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
          line-height: 14px
          margin-bottom: 8px
          font-size: 14px
          font-weight: 700
          color: rgb(7, 17, 27)
        .food-detail
          margin-bottom: 18px
          height: 10px
          line-height: 10px
          font-size: 0
          .sell-count, .rating
            font-size: 10px
            color: rgb(147, 153, 153)
          .sell-count
            margin-right: 12px
         .price
           font-weight: 700
           line-height: 24px
           .now
            margin-right: 8px
            font-size: 14px
            color: rgb(240, 20 ,20)
          .old
            text-decoration: line-through
            font-size: 10px
            color: rgb(147, 153, 159)
        .cartcontrol-wrapper
          position: absolute
          right: 12px
          bottom: 12px
        .buy
          position: absolute
          right: 18px
          bottom: 18px
          z-index: 10
          height: 24px
          line-height: 24px
          padding: 0 12px
          box-sizing: border-box
          border-radius: 12px
          font-size: 10px
          color: #fff
          background: rgb(0, 160, 220)
          &.fade-transition
            transition: all 0.2s
            opacity: 1
          &.fade-enter, &.fade-leave
            opacity: 0
      .info
        padding: 18px
        .title
          line-height: 14px
          margin-bottom: 6px
          font-size: 14px
          font-weight: 700
          color: rgb(7, 17, 27)
        .text
          line-height: 24px
          padding: 0 8px
          font-size: 12px
          color: rgb(77, 85, 93)
</style>
