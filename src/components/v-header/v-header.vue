<template>
  <div class="header" @click="showDetail">
    <div class="content-wrapper">
      <div class="avatar">
        <img width="64" height="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div v-if="seller.supports" class="support">
          <support-ico :size=1 :type="seller.supports[0].type"></support-ico>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail">
        <span class="count">{{seller.supports.length}}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <!-- <img :src="seller.avatar" width="100%" height="100%"> -->
    </div>
     <div v-show="detailShow" class="detail">
       <div class="detail-wrapper clearfix">
         <div class="detail-main">
           <h1 class="name">{{seller.name}}</h1>
           <div class="star-wrapper">
             <star :size="48" :score="seller.score" class="start"></star>
           </div>
           <div class="title">
             <div class="line"></div>
             <div class="text">优惠信息</div>
             <div class="line"></div>
           </div>
           <ul v-if="seller.supports" class="supports">
             <li class="support-item" v-for="(item,index) in seller.supports " :key="index">
               <span class="icon" :class="classMap[item.type]"></span>
               <span class="text" >{{item.description}}></span>
             </li>
           </ul>
           <div class="des">
             <div class="line1"></div>
             <div class="text1">商家公告</div>
             <div class="line1"></div>
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

<script type="text/ecmascript-6">
import SupportIco from 'components/support-ico/support-ico.vue'
import Star from 'components/star/star.vue'

export default {
  name: 'v-header',
  props: {
    seller: {
      type: Object,
      default () {
        return {}
      }
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      // this.headerDetailComp = this.headerDetailComp || this.$createHeaderDetail({
      //   $props: {
      //     seller: 'seller'
      //   }
      // })
      // this.headerDetailComp.show()
      this.detailShow = true
    },
    hideDetail (e) {
      e.stopPropagation()
      this.detailShow = false
    }
  },
  created () {
    this.classMap = [ 'decrease', 'discount', 'special', 'invoice', 'gunrantee' ]
  },
  components: {
    SupportIco,
    Star
  }
}
</script>

<style lang="stylus">
  @import "~common/stylus/mixin"
  @import "~common/stylus/variable"

  .header
    position: relative
    overflow: hidden
    color: $color-white
    background: $color-background-ss
    .content-wrapper
      position: relative
      display: flex
      align-items: center
      padding: 24px 12px 18px 24px
      .avatar
        flex: 0 0 64px
        width: 64px
        margin-right: 16px
        img
          border-radius: 2px
      .content
        flex: 1
        .title
          display: flex
          align-items: center
          margin-bottom: 8px
          .brand
            width: 30px
            height: 18px
            bg-image('brand')
            background-size: 30px 18px
            background-repeat: no-repeat
          .name
            margin-left: 6px
            font-size: $fontsize-large
            font-weight: bold
        .description
          margin-bottom: 8px
          line-height: 12px
          font-size: $fontsize-small
        .support
          display: flex
          align-items: center
          .support-ico
            margin-right: 4px
          .text
            line-height: 12px
            font-size: $fontsize-small-s

      .support-count
        position: absolute
        right: 12px
        bottom: 14px
        display: flex
        align-items: center
        padding: 0 8px
        height: 24px
        line-height: 24px
        text-align: center
        border-radius: 14px
        background: $color-background-sss
        .count
          font-size: $fontsize-small-s
        .icon-keyboard_arrow_right
          margin-left: 2px
          line-height: 24px
          font-size: $fontsize-small-s

    .bulletin-wrapper
      position: relative
      display: flex
      align-items: center
      height: 28px
      line-height: 28px
      padding: 0 8px
      background: $color-background-sss
      .bulletin-title
        flex: 0 0 22px
        width: 22px
        height: 12px
        margin-right: 4px
        bg-image('bulletin')
        background-size: 22px 12px
        background-repeat: no-repeat
      .bulletin-text
        flex: 1
        white-space: nowrap
        overflow: hidden
        text-overflow: ellipsis
        font-size: $fontsize-small-s
      .icon-keyboard_arrow_right
        flex: 0 0 10px
        width: 10px
        font-size: $fontsize-small-s
    .background
      position: absolute
      top: 0
      left: 0
      width: 100%
      height: 100%
      z-index: -1
      filter: blur(10px)
    .detail
      position: fixed
      z-index: 100
      top: 0
      left: 0
      width: 100%
      height:100%
      overflow: auto
      background: rgba(7,17,27,0.8)
      .detail-wrapper
        min-height:100%
        width: 100%
        .detail-main
          padding-top: 64px
          padding-bottom: 64px
          .name
            line-height: 16px
            text-align: center
            font-size: 16px
            font-weight: 700
            color: white
          .star-wrapper
            text-align: center
            margin-top: 18px
            padding: 2px 0
          .title
            display: flex
            width: 80%
            margin: 28px auto 24px auto
            .line
              flex: 1
              position: relative
              top: -6px
              border-bottom: 1px solid rgba(255,255,255,0.2)
            .text
              padding: 0 12px
              font-size: 14px
              font-weight: 700
              color: white
          .supports
            width: 80%
            margin: 0 auto
            .support-item
              padding: 0 12px
              margin-bottom: 12px
              font-size: 0
              &:last-child
                margin-bottom: 0
              .icon
                display: inline-block
                width: 16px
                height: 16px
                vertical-align: top
                margin-right: 6px
                background-size: 16px 16px
                background-repeat: no-repeat
                &.decrease
                  bg-image('decrease_2')
                &.discount
                  bg-image('discount_2')
                &.gunrantee
                  bg-image('guarantee_2')
                &.invoice
                  bg-image('invoice_2')
                &.special
                  bg-image('special_2')
              .text
                line-height: 12px
                font-size: 12px
                color: white
        .des
            display: flex
            width: 80%
            margin: 28px auto 24px auto
            .line1
              flex: 1
              position: relative
              top: -6px
              border-bottom: 1px solid rgba(255,255,255,0.2)
            .text1
              padding: 0 12px
              font-size: 14px
              font-weight: 700
              color: white
        .bulletin
            width: 80%
            margin: 0 auto
            .content
              padding: 0 12px
              line-height: 24px
              font-size: 12px
              color: white
      .detail-close
        position: relative
        width: 32px
        height: 32px
        line-height: 32px
        margin: -64px auto 0 auto
        clear: both
        color: rgba(255,255,255,0.8)
        font-size: 32px
</style>
