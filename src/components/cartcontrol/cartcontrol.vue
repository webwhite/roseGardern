<template>
  <div class="cartcontrol">
      <transition name="move">
        <div @click="decrease" v-show="food.count>0" class="cart-decrease icon-remove_circle_outline">
            <!-- <span class="inner icon-remove_circle_outline"></span> -->
        </div>
      </transition>
      <div v-show="food.count>0" class="cart-count">{{food.count}}</div>
      <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue'
export default {
    props: {
        food: {
            type: Object
        }
    },
    methods: {
        addCart() {
            if (!this.food.count) {
                Vue.set(this.food, 'count', 1)
            } else {
               this.food.count++ 
            }   
        },
         decrease() {
             if(this.food.count){
                 this.food.count--
             }
        } 
    }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
    font-size 0
    .cart-decrease
        display inline-block
        transform translate3d(0,0,0) rotate(-180deg)
        font-size 24px
        padding 6px
        color rgb(0,160,220)
        opacity 1
        &.move-enter,&.move-leave-to
            opacity 0
            transform translate3d(24px,0,0) rotate(0)
        &.move-enter-active,&.move-leave-active
            transition all 0.4s linear
    .cart-count
        display:inline-block
        vertical-align top
        width 12px
        font-size 10px
        color rgb(147,153,159)
        text-align center
        line-height 36px
    .cart-add
        display inline-block
        padding 6px
        line-height 24px
        font-size 24px
        color rgb(0,160,220)
</style>
