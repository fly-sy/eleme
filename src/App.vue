<template>
  <div class="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item border-1px">
        <a v-link="{path: '/goods'}">商品</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/ratings'}">评论</a>
      </div>
      <div class="tab-item">
        <a v-link="{path: '/seller'}">商家</a>
      </div>
    </div>
    <!-- 渲染路由组件 -->
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
import VHeader from './components/header/header';
const ERR_OK = 0;
export default {
  data: ()=>({
    seller: {}
  }),
  created() {
    this.$http.get('api/seller').then((res)=>{
      res = res.body;
      if(res.errno === ERR_OK){
        this.seller = res.data;
      }
    });
  },
  components: {
    VHeader
  }
}
</script>

<style lang="stylus">
  @import "./common/stylus/mixin";

  .app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7 ,17, 27, 0.1))
      .tab-item
        flex: 1
        text-align: center
        & > a
          display: block
          color: rgb(77, 85, 93);
          &.active
            color: red
</style>
