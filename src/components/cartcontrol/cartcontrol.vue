<template>
  <div class="cartcontrol">
    <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0"></div>
    <div class="cart-count"  v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>
<script>
import Vue from 'vue'
export default {
  props: {
    food: {
      type: Object
    }
  },
  created () {
  },
  methods: {
    addCart () {
      console.log('click')
      if (!this.food.count > 0) {
        Vue.set(this.food, 'count', 1)
      } else {
        this.food.count++
      }
    }
  }
}
</script>
<style lang="stylus">
@import "~common/stylus/mixin"
@import "~common/stylus/variable"
  .cartcontrol
    font-size: 0
    .cart-decrease, .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
    .cart-count
      display: inline-block
      font-size: 10px
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 10px
      text-align: center
      color: gray   
</style>
