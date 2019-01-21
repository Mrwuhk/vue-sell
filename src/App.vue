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
        <router-link active-class="a" to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header.vue'
const ERR_OK = 0
export default {
  data () {
    return {
      sellers: {}
    }
  },
  created () {
    this.$http.get('./api/seller').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.seller = response.data
        console.log(this.seller)
      }
    })
  },
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
      border-bottom: 1px solid  rgba(7,17,27,0.1)
      .tab-item
        flex: 1
        text-align: center
        & > .a
          display: block
          font-size: 14px
          color: rgba(77,85,93,1)
          text-decoration: none
</style>
