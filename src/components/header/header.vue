<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" alt="" width="64" height="64">
      </div>
      <div class="content">
        <div class="title">
        <span class="brand"></span>
        <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliverytime}}分钟送达
        </div>
        <div v-if="seller.supports" class="supports decrease">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="support-count" v-if="seller.supports" @click="showDetail">
        <span class="count">{{seller.supports.length}}</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper" @click="showDetail">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="bg">
      <img :src="seller.avatar" alt="" width="100%" height="100%">
    </div>
    <!-- <div class="detail" v-show="detailShow" transition="fade"> -->
    <div class="detail" v-show="detailShow">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
          <h1 class="name">{{seller.name}}</h1>
          <div class="star-wrapper">
            <star :size="48" :score="seller.score"></star>
          </div>
          <div class="title">
            <div class="line"></div>
            <div class="text">优惠信息</div>
            <div class="line"></div>
          </div>
          <ul v-if="seller.supports" class="supports">
            <li class="support-item" v-for="item in seller.supports">
              <span class="icon" :class="classMap[seller.supports[$index].type]"></span>
              <span class="text">{{seller.supports[$index].description}}</span>
            </li>
          </ul>
          <div class="title">
            <div class="line"></div>
            <div class="text">商家公告</div>
            <div class="line"></div>
          </div>
          <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
          </div>
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>

<script>
  import star from '../star/star';

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data: ()=>({
      detailShow: false
    }),
    methods: {
      showDetail() {
        this.detailShow = true;
      },
      hideDetail() {
        this.detailShow = false;
      }
    },
    components: {
      star
    },
    created() {
      this.classMap = ['decrease','discount','special','invoice','guarantee'];
    }
  }
</script>

<style lang="stylus">
  @import "../../common/stylus/mixin";

  .header
    position: relative
    color: #fff
    background: rgba(7, 17, 27, 0.5)
    overflow: hidden
   .content-wrapper
      position: relative
      padding: 24px 12px 18px 24px
      font-size: 0
      .avatar
        display: inline-block
        vertical-align: top
        img
          border-radius: 2px
      .content
        display: inline-block
        margin-left: 16px
        font-size: 14px
        .title
          margin: 2px 0 8px 0
          .brand
            display: inline-block
            vertical-align: top
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: 16px
            font-weigth: bold
            line-height: 18px
        .description
          margin-bottom: 10px
          line-height: 12px
          font-size: 12px
        .supports
          font-size: 0
          .icon
            display: inline-block
            vertical-align: top
            width: 12px
            height: 12px
            margin-right: 4px
            background-size: 12px 12px
            background-repeat: no-repeat
            &.decrease
              bg-image('decrease_1')
            &.discount
              bg-image('discount_1')
            &.decrease
              bg-image('decrease_1')
            &.guarantee
              bg-image('guarantee_1')
            &.invoice
              bg-image('invoice_1')
            &.special
              bg-image('special_1')
          .text
            line-height: 12px
            font-size: 12px
      .support-count
        position: absolute
        right: 12px
        bottom: 18px
        padding: 0 8px
        height: 24px
        line-height: 24px
        font-size: 10px
        background: rgba(0, 0, 0, 0.2)
        border-radius: 14px
        text-align: center
        .count
        .icon-keyboard_arrow_right
          margin-left: 2px
          line-height: 24px
   .bulletin-wrapper
    position: relative
    height: 28px
    line-height: 28px
    padding: 0 22px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background: rgba(7, 17, 27, 0.2)
    .bulletin-title
      display: inline-block
      vertical-align: top
      margin-top: 9px
      width: 22px
      height: 12px
      bg-image('bulletin')
      background-size: 22px 12px
      background-repeat: no-repeat
    .bulletin-text
      margin: 0 4px
      font-size: 12px
    .icon-keyboard_arrow_right
      position: absolute
      font-size: 10px
      right: 12px
      top: 12px
   .bg
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    z-index: -1
    filter: blur(10px)
   .detail
      position: fixed
      top: 0
      left: 0
      z-index: 100
      width: 100%
      height: 100%
      overflow: auto
      transition: all 1s ease
      background: rgba(7, 17, 27 0.8)
      /*&.fade-transition
        opcity: 1
        background: rgba(7, 17, 27 0.8)
      &.fade-enter, &.fade-leave
        opcity: 0
        background: rgba(7, 17, 27 0)*/
    .detail-wrapper
      min-height: 100%
      width: 100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
      .name
        line-height: 16px
        text-align: center
      .star-wrapper
        margin-top: 18px
        padding: 2px 0
        text-align: center
      .title
        display: flex
        width: 80%
        margin: 28px auto 24px auto
        .line
          flex: 1
          position: relative
          top: -6px
          border-bottom: 1px solid rgba(255, 255, 255, 0.2)
        .text
          padding: 0 12px
          font-size: 14px
          font-weight: 700
      .supports
        width: 80%
        margin: 0 auto
        .support-item
          padding: 0 12px
          margin-bottom: 12px
          font-size: 0
          &:last-child
            margin-right: 0
          .icon
            display: inline-block
            vertical-align: top
            width: 16px
            height: 16px
            margin-right: 6px
            background-size: 16px 16px
            background-repear: no-repeat
            &.decrease
              bg-image('decrease_2')
            &.discount
              bg-image('discount_2')
            &.decrease
              bg-image('decrease_2')
            &.guarantee
              bg-image('guarantee_2')
            &.invoice
              bg-image('invoice_2')
            &.special
              bg-image('special_2')
          .text
            line-height: 16px
            font-size: 12px
      .bulletin
        width: 80%
        margin: 0 auto
        .content
          padding: 0 12px
          line-height: 24px
          font-size: 12px
          text-indent: 2em


    .detail-close
      position: relative
      width: 32px
      height: 32px
      margin: -64px auto 64px auto
      clear: both
      font-size: 32px


</style>
