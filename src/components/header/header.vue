<template>
  <div class="header">
    <div class="content-wraper">
      <div class="avatar">
        <img height="64" width="64" :src="seller.avatar">
      </div>
      <div class="content">
        <div class="title">
          <div class="brand"></div>
          <div class="name">{{ seller.name }}</div>
        </div>
        <div class="description">
          {{ seller.description }}/{{ seller.deliveryTime }}分送达
        </div>
        <div v-if="seller.supports" class="supports">
          <div class="icon" :class="classMap[seller.supports[0].type]"></div>
          <div class="text">{{ seller.supports[0].description }}</div>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count" @click="showDetail()">
        <div class="count">{{ seller.supports.length }}个</div>
        <div class="icon-keyboard_arrow_right"></div>
      </div>
    </div>
    <div class="bulletin-wraper" @click="showDetail()">
      <span class="bulletin-title"></span><span class="bulletin-text">{{ seller.bulletin }}</span>
      <div class="icon-keyboard_arrow_right"></div>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%">
    </div>
    <div v-show="detailShow" class="detail">
      <div class="detail-wraper clearfix">
        <div class="detail-main">
          <h1 class="name">{{ seller.name }}</h1>
          <star :size="48" :score="seller.score"></star>
        </div>
      </div>
      <div class="detail-close">
        <i class="icon-close"></i>
      </div>
    </div>
  </div>
</template>

<script>
import Star from 'components/star/star'
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data () {
    return {
      detailShow: false
    }
  },
  methods: {
    showDetail () {
      this.detailShow = true
    }
  },
  created () {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  },
  components: {
    Star
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import '../../common/stylus/mixin.styl'
.header
  position: relative
  color: #fff
  overflow: hidden
  background: rgba(7,17,27,0.5)
  .content-wraper
    position: relative
    padding: 24px 12px 18px 24px
    font-size: 0
    .avatar
      vertical-align: top
      display: inline-block
      img
        border-radius: 2px
    .content
      margin-left: 16px
      display: inline-block
      .title
        margin: 2px 0 8px 0
        .brand
          vertical-align: top
          display: inline-block
          width: 30px
          height: 18px
          bg-image('brand')
          background-size: 30px 18px
          background-repeat: no-repeat
        .name
          display: inline-block
          margin-left: 6px
          font-weight: bold
          line-height: 18px
          color: rgb(255,255,255)
          font-size: 16px
      .description
        margin-bottom: 10px
        line-height: 12px
        font-size: 12px
        font-weight: 200
      .supports
        margin-bottom: 2px
        .icon
          vertical-align: top
          display: inline-block
          width: 12px
          height: 12px
          background-size: 12px 12px
          background-repeat: no-repeat
          &.decrease
            bg-image('decrease_1')
          &.discount
            bg-image('discount_1')
          &.special
            bg-image('special_1')
          &.invoice
            bg-image('invoice_1')
          &.guarantee
            bg-image('guarantee_1')
        .text
          margin-left: 4px
          font-size: 10px
          font-weight: 200
          line-height: 12px
          display: inline-block
    .support-count
      position: absolute
      right: 12px
      bottom: 14px
      height: 24px
      padding: 0 8px
      line-height: 24px
      border-radius: 14px
      background-color: rgba(0,0,0,0.2)
      text-align: center
      .count
        vertical-align: top
        display: inline-block
        font-size: 10px
      .icon-keyboard_arrow_right
        font-size: 10px
        line-height: 24px
        margin-left: 2px
        display: inline-block
  .bulletin-wraper
    position: relative
    height: 28px
    line-height: 28px
    padding: 0 22px 0 12px
    white-space: nowrap
    overflow: hidden
    text-overflow: ellipsis
    background-color: rgba(7,17,27,0.2)
    .bulletin-title
      margin-top: 8px
      vertical-align: top
      display: inline-block
      width: 22px
      height: 12px
      bg-image('bulletin')
      background-size: 22px 12px
      background-repeat: no-repeat
    .bulletin-text
      vertical-align: top
      margin: 0 4px
      font-size: 10px
      font-weight: 200
    .icon-keyboard_arrow_right
      vertical-align: top
      position: absolute
      display: inline-block
      font-size: 10px
      right: 12px
      top: 9px
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
    top: 0
    left: 0
    z-index: 100
    width: 100%
    height: 100%
    overflow: auto
    background-color: rgba(7,17,27,0.8)
    .detail-wraper
      min-height: 100%
      width: 100%
      .detail-main
        margin-top: 64px
        padding-bottom: 64px
        text-align: center
        .name
          line-height: 64px
          font-size: 16px
          font-weight: 700
    .detail-close
      position: relative
      width: 32px
      height: 32px
      margin: -64px auto 0 auto
      clear: both
      font-size: 32px
</style>
