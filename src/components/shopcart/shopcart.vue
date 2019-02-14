<template>
  <div class="shopcart">
    <div class="content" @click="toggleList">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount>0}">
            <i class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></i>
          </div>
          <div class="num" v-show="totalCount>0">{{totalCount}}</div>
        </div>
        <div class="price" :class="{'highlight':totalPrice>0}">¥{{totalPrice}}元</div>
        <div class="desc">另需配送费¥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">{{payDesc}}</div>
      </div>
    </div>
    <!-- <div class="ball-container">
      <div v-for="(ball,index) in balls" :key="index" v-show="ball.show" transition="drop" class="ball">
        <div class="inner"></div>
      </div>
    </div> -->
    <transition name="fold">
      <div v-show="listShow" :class="['shopcart-list', {'active': listShow}]">
        <div class="list-hearder">
          <h1 class="title">购物车</h1>
          <span class="empty">清空</span>
        </div>
        <div class="list-content">
          <ul>
            <li class="food" v-for="(food,index) in  selectFoods" :key="index">
              <span class="name">{{food.name}}</span>
              <div class="price">
                <span>¥{{food.price*food.count}}</span>
              </div>
              <div class="cartcontrol-wrapper">
                <cartcontrol :food="food"></cartcontrol>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </transition>
  </div>
</template>
<script>
import cartcontrol from 'components/cartcontrol/cartcontrol.vue'
export default {
  props: {
    selectFoods: {
      type: Array,
      default () {
        return []
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      fold: true
    }
  },
  methods: {
    toggleList () {
      if (this.totalCount === 0) {
        this.fold = true
        return
      }
      this.fold = !this.fold
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFoods.forEach((food) => {
        count += food.count
      })
      return count
    },
    payDesc () {
      if (this.totalPrice === 0) {
        return `¥${this.minPrice}元起送`
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return `还差¥${diff}元起送`
      } else {
        return `去结算`
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    },
    listShow () {
      if (this.totalCount === 0) {
        this.fold = true
        return false
      }
      return !this.fold
    }
  },
  components: {
    cartcontrol
  }
}
</script>
<style lang="stylus">
@import "~common/stylus/mixin"
@import "~common/stylus/variable"
.shopcart
  position: fixed
  left: 0
  bottom: 0
  z-index: 50
  width: 100%
  height: 48px
  .content
    display: flex
    background: #141d27
    font-size: 0
    color: rgba(255,255,255,0.4)
    .content-left
      flex: 1
      .logo-wrapper
        display: inline-block
        position: relative
        top: -10px
        margin: 0 12px
        padding: 6px
        width: 56px
        height: 56px
        box-sizing: border-box
        vertical-align: top
        border-radius: 50%
        background:  #141d27
        .logo
          width: 100%
          height: 100%
          border-radius: 50%
          text-align: center
          background: #2b343c
          &.highlight
            background: rgb(0,160,220)
          .icon-shopping_cart
            font-size: 24px
            line-height: 44px
            color: #80858a
            &.highlight
              color: #fff
        .num
          position: absolute
          top: 0
          right: 0
          width: 24px
          height: 16px
          line-height: 16px
          text-align:  center
          font-size: 9px
          border-radius: 16px
          font-weight: 700
          color: white
          background: red
          box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4)
      .price
        display: inline-block
        vertical-align: top
        line-height: 24px
        margin-top: 12px
        padding-right: 12px
        border-right: 1 solid rgba(255,255,255,0.4)
        font-size: 16px
        font-weight: 700
        &.highlight
          color: white
      .desc
        display: inline-block
        vertical-align: top
        line-height: 24px
        margin: 12px 0 0 12px
        font-size: 10px
    .content-right
      flex: 0 0 105px
      width: 105px
      .pay
        height: 48px
        line-height: 48px
        text-align: center
        font-size: 12px
        font-weight: 700
        &.not-enough
          background: rgba(255,255,255,0.4)
        &.enough
          background: #00b432
          color: #fff
  .ball-container
    .ball
      position: fixed 
      left: 32px
      bottom: 22px
      z-index: 200
      &.drop-transition
        transition: all 0.5s
        .inner
          width: 16px
          height: 16px
          border-radius: 50%
          color: rgb(0,160,220)
          transition: all 0.5s
  .fold-enter-active, .fold-leave-active
    transition: all 10s
  .fold-enter, .fold-leave-to
    transform: translate3d(0,0,0)
  .shopcart-list
    position: absolute
    top: 0
    left: 0
    z-index: 100
    width: 100%
    transform: translate3d(0,-100%,0)
    // &.active
    //   top: auto
    //   bottom: 56px
    //   z-index: 100
    // &.fold-transition
    //   transition: all 0.5s
    //   transform: translate3d(0,-100%,0)
    // &.fold-enter,&.fold-leave
    //   transform: translate3d(0,0,0)
    .list-hearder
      height: 40px
      line-height: 40px
      padding: 0 18px
      background: #f3f5f7
      border-bottom: 1px solid rgba(7,17,27,0.1)
      .title
        float: left
        font-size: 14px
        color: rgb(7,17,27)
      .empty
        float: right
        font-size: 12px
        color: rgb(0,160,220)
</style>
