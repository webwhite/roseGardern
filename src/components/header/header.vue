<template>
  <div class="header">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" width=64 height=64>
      </div>
      <div class="content">
        <div class="title">
          <span class="brand"></span>
          <span class="name">{{seller.name}}</span>
        </div>
        <div class="description">
          {{seller.description}}/{{seller.deliveryTime}}分钟到达
        </div>
        <div v-if="seller.supports" class="support">
          <span class="icon" :class="classMap[seller.supports[0].type]"></span>
          <span class="text">{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div v-if="seller.supports" class="support-count">
          <span class="count">{{seller.supports.length}}/个</span>
          <i class="icon-keyboard_arrow_right"></i>
      </div>
    </div>
    <div class="bulletin-wrapper">
      <span class="bulletin-title"></span>
      <span class="bulletin-text">{{seller.bulletin}}</span>
      <i class="icon-keyboard_arrow_right"></i>
    </div>
    <div class="background">
      <img :src="seller.avatar" width="100%" height='100%'>
    </div>
    <transition name="fade">
      <div class="detail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper"></div>
            <div class="title">
              <span class="line"></span><span class="text">优惠信息</span><span class="line"></span>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li class="support-item" v-for="(item ,index) in seller.supports" :key='index'>
                <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <span class="line"></span><span class="text">商家公告</span><span class="line"></span>
            </div>
            <div class="bulletin"><p class="content">{{seller.bulletin}}</p></div>
          </div>
        </div>
        <div class="detail-close">
          <i class="icon-close"></i>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["seller"],
  created() {
    this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']
  }
};
</script>

<style lang='stylus' rel='sheetstyle/stylus'>
@import '../../common/stylus/mixin.styl';
.header
  position relative
  width: 100%;
  color: rgb(255, 255, 255);
  background rgba(7,17,27,0.5)
  .content-wrapper
    position relative
    padding:24px 12px 18px 24px
    font-size 0
    .avatar
      display inline-block
      vertical-align top
      img
        border-radius 2px
    .content
      display inline-block
      margin-left 16px
      font-size 14px
      .title
       margin 2px 0 8px 0
       .brand
        display inline-block
        vertical-align top
        width:30px
        height 18px
        bg-image('brand')
        background-size 30px 18px
        background-repeat no-repeat
       .name
        margin-left 6px
        font-size 16px
        line-height 18px
        font-weight bold
      .description
        margin-bottom: 10px
        line-height: 12px
        font-size: 12px
      .support
       .icon
        display: inline-block
        width: 14px
        height: 14px
        vertical-align: top
        margin-right: 6px
        background-size: 14px 14px
        background-repeat: no-repeat
        &.decrease
          bg-image('decrease_2')
        &.discount
          bg-image('discount_2')
        &.guarantee
          bg-image('guarantee_2')
        &.invoice
          bg-image('invoice_2')
        &.special
          bg-image('special_2')
       .text
        line-height: 16px
        font-size: 12px
    .support-count
     position:absolute
     right 12px
     bottom 18px
     padding 0 8px
     height 24px
     line-height 24px
     border-radius 14px
     background-color: rgba(0,0,0,0.2)
     text-align center
     .count
      font-size 10px
      vertical-align top
     .icon-keyboard_arrow_right
      line-height 24px
      margin-left 2px
      font-size 10px

  .bulletin-wrapper
   position relative
   height 28px
   line-height 28px
   padding-right 22px
   background-color rgba(7,17,27,0.2)
   white-space: nowrap
   overflow: hidden
   text-overflow: ellipsis
   .bulletin-title
    display inline-block
    vertical-align middle
    width 22px
    height 12px
    margin-left 12px
    background-size 22px 12px
    background-repeat no-repeat
    bg-image('bulletin')
   .bulletin-text
    margin 0 4px
    font-size 10px
    font-weight 200
   .icon-keyboard_arrow_right
    position absolute
    right 12px
    top 8px

  .background
   position absolute
   top 0
   left 0
   z-index -1
   width 100%
   height 100%
   filter blur(10px)

  .detail
   position fixed
   top 0
   left 0
   z-index 100
   width 100%
   height 100%
   background rgba(7,17,27,0.8)
   .detail-wrapper
    width:100%
    min-height:100%
    .detail-main
      margin 64px 0
      .name
        line-height 16px
        text-align center
        font-size 16px
        font-weight 700
      .star-wrapper
        margin-top 18px
        padding 2px 0
        text-align center
      .title
        margin 28px auto 24px auto
        width:80%
        display flex
      .line
        position relative
        flex 1
        top -6px
        border-bottom 1px solid rgba(255,255,255,0.2)
      .text
        font-size 14px
        font-weight 700
        padding 0 12px
        text-align center
      .supports
        width:80%
        margin 0 auto
        .support-item
          margin 0 12px
          margin-bottom 12px
          font-size 0
          &:last-child
            margin-bottom 0
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
            &.guarantee
              bg-image('guarantee_2')
            &.invoice
              bg-image('invoice_2')
            &.special
              bg-image('special_2')
          .text
            line-height: 16px
            font-size: 12px

      .bulletin
        width 80%
        margin 0 auto
      .content
        padding 0 12px
        font-size 12px
        line-height 24px
  .detail-close
    position relative
    width 32px
    height 32px
    margin -64px auto 0 auto
    font-size 32px
    clear both
</style>
