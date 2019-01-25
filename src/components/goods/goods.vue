<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li v-for="(item,index) in goods" :key="index" class="menu-item">
          <span class="text border-1px">
             <span v-show= "item.type>0" class="icon" :class="classMap[item.type]"></span>
            {{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li v-for="(item,index) in goods" :key="index" class="food-list">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="(food,index) in item.foods" :key="index" class="food-item border-1px">
              <div class="icon">
                <img :src="food.icon" width="57px" height="57px">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span>月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span>¥{{food.price}}</span>
                  <span v-show="food.oldPrice">¥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
const ERR_OK = 0
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      goods: []
    }
  },
  created () {
    this.classMap = [ 'decrease', 'discount', 'special', 'invoice', 'gunrantee' ]
    this.$http.get('./api/goods').then((response) => {
      response = response.body
      if (response.errno === ERR_OK) {
        this.goods = response.data
      }
    })
  }
}
</script>
<style lang="stylus">
@import "~common/stylus/mixin"
@import "~common/stylus/variable"
  .goods
    display: flex
    position: absolute
    top: 179px
    bottom: 46px
    width: 100%
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      width: 80px
      background: #f3f5f7
      .menu-item
        display: flex
        height: 54px
        width: 100%
        .icon
          display: inline-block
          width: 12px
          height: 12px
          vertical-align: top
          margin-right: 2px
          background-size: 12px 12px
          background-repeat: no-repeat
          overflow: hidden
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.gunrantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
        .text
          font-size: 12px
          width: 100%
          display: flex
          justify-content: center
          align-items: center
          list-style-type: none
          border-1px(rgba(7,17,27,0.1))
    .foods-wrapper
      flex: 1
      .food-list,.item-food
        list-style-type: none
      .title
        padding-left: 14px
        height: 26px
        line-height: 26px
        border-left: 2px solid #d9ddb1
        font-size: 12px
        color: rgb(147,153,159)
        background: #f3f5f7
      .food-item
        display: flex
        margin: 18px
        padding-bottom: 18px
        border-1px(rgba(7,17,27,0.1))
        &:last-child
          border-none()
          margin-bottom: 0
        .icon
          felx: 0 0 57px
          margin-right: 10px
        .content
          flex: 1
          .name
            margin: 2px 0 8px 0
            height: 14px
            line-height: 14px
            font-size: 14px
          .desc,.extra
            line-height: 10px
            font-size: 10px
            color: rgb(147,153,159)
          .desc
            margin-bottom: 8px
          .extra
            &.content
              margin-right: 12px

</style>
