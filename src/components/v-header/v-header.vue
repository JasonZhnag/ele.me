<template>
  <div class="header" @click="detailShow">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" height="64" width="64" />
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{ seller.name }}</span>
        </div>
        <div class="description">{{ seller.description }}/{{ seller.deliveryTime }}分钟送达</div>
        <div class="support" v-if="seller.supports">
          <support-ico :type="seller.supports[0].type" :size="size" class="icon"></support-ico>
          <span class="text">{{ seller.supports[0].description }}</span>
        </div>
      </div>
      <div class="support-count" v-if="seller.supports" @click="detailShow">
        <span class="count">{{ seller.supports.length }}个</span>
        <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{ seller.bulletin }}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height="100%" />
    </div>
  </div>
</template>
<script>
import SupportIco from 'components/support-ico/support-ico'

export default {
  name: 'v-header',
  props: {
    seller: {
      type: Object,
      default() {
        return {}
      }
    }
  },
  data() {
    return {
      size: 1
    }
  },
  methods: {
    detailShow() {
      this.headerDetailComp = this.headerDetailComp || this.$createHeaderDetail({
        $props: {
          seller: 'seller'
        }
      })
      this.headerDetailComp.show()
    }
  },
  components: {
    SupportIco
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/mixin'
@import '~common/stylus/variable'
.header
  position relative
  overflow hidden
  color $color-white
  background $color-background-ss
  .content-wrapper
    position relative
    padding 24px 12px 18px 24px
    font-size 0
    .avatar
      vertical-align top
      display inline-block
      img
        border-radius 2px
    .content
      display inline-block
      margin-left 16px
      font-size $fontsize-medium
      .title
        margin 2px 0 8px 0
        .brand
          vertical-align top
          display inline-block
          width 30px
          height 18px
          bg-image('brand')
          background-size 30px 18px
          background-repeat no-repeat
        .name
          font-size $fontsize-large
          font-weight bold
          line-height 18px
          margin-left 6px
      .description
        font-size $fontsize-small
        margin-bottom 10px
      .support
        .icon
          margin-right 4px
        .text
          font-size $fontsize-small-s
          line-height 12px
    .support-count
      position absolute
      right 12px
      bottom 18px
      height 24px
      padding 0 8px
      background rgba(0, 0, 0, 0.2)
      text-align center
      border-radius 14px
      .count
        font-size $fontsize-small-s
        border none
      .icon-keyboard_arrow_right
        margin-left 2px
        line-height 24px
        font-size $fontsize-small-s
  .bulletin-wrapper
    background $color-background-sss
    position relative
    height 28px
    line-height 28px
    padding 0 22px 0 12px
    white-space nowrap
    overflow hidden
    text-overflow ellipsis
    .bulletin-title
      vertical-align top
      margin-top 8px
      display inline-block
      margin-right 4px
      width 22px
      height 12px
      bg-image 'bulletin'
      background-size 22px 12px
      background-repeat no-repeat
    .bulletin-text
      font-size $fontsize-small-s
      line-height 28px
    .icon-keyboard_arrow_right
      position absolute
      right 12px
      top 8px
      font-size $fontsize-small-s
      margin-left 4px
  .background
    position absolute
    left 0
    top 0
    width 100%
    height 100%
    z-index -1
    filter blur(10px)
</style>