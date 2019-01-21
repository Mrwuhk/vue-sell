<template>
  <div id="app">
    <v-header></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link active-class="a" to="/goods">商品</router-link>
        </div>
      <div class="tab-item">
        <router-link active-class="a" to="/ratings">评论</router-link>
        </div>
      <div class="tab-item">
        <router-link active-class="a" to="/sellers">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header.vue'
export default {
  components: {
    VHeader
  }
}
</script>

<style lang="stylus">
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      .tab-item
        flex: 1
        text-align: center
        & > .a
          display: block
          background-color: red
          text-decoration: none

</style>
