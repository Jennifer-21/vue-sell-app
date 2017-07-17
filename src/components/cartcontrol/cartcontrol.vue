<template>
  <div class="cartControl">
    <transition name="move">
      <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click.stop.prevent="decreaseCart">
        <!--<span class="inner icon-remove_circle_outline"></span>-->
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart">
      <transition @click="show=!show" name="slide-fade"></transition>
    </div>
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
//    created () {
//      console.log(this.food)
//    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
          return
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count++
        }
        this.$emit('cartAdd', event)
      },
      decreaseCart (event) {
        if (!event._constructed) {
          return
        }
        if (this.food.count) {
          this.food.count--
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartControl
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
      transform translate3d(0, 0, 0) rotate(0)
      &.move-enter-active, &.move-leave-active
        transition: all 0.4s linear
      /*.inner
        transition all 1s*/
      &.move-enter, &.move-leave-active
        opacity: 0
        transform: translate3d(24px, 0, 0) rotate(180deg)
    /*.inner
      transform rotate(180deg)*/
    /*.inner
      display inline-block
      transform rotate(0)*/

    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>
