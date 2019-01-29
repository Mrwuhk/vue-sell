<template>
  <div class="cartcontrol">
    <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart" transition="move">
      <span class="inner icon-remove_circle_outline"></span>
    </div>
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
    decreaseCart () {
      if (this.food.count > 0) {
        this.food.count--
      }
    },
    addCart () {
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
    .cart-decrease
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      &.move-transition
        opacity: 1
        transform: translate3D(0,0,0)
      .inner
        display: inline-block
        line-height: 24px
        font-size: 24px
        color: rgb(0,160,220)
        transition: all 0.4s linear
      &.move-enter,&move-leave
        opacity: 0
        transform: translate3D(24px,0,0)
    .cart-count
      display: inline-block
      font-size: 10px
      vertical-align: top
      width: 12px
      padding-top: 12px
      line-height: 10px
      text-align: center
      color: gray
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0,160,220)
</style>
