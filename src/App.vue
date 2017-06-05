<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods" class="a">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings" class="a">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller" class="a">商家</router-link>
      </div>

    </div>
    <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue'
  const ERR_OK = 0
  export default {
    data () {
      return {
        seller: {}
      }
    },
    created () {
      this.$http.get('/api/seller?id=' + this.seller.id).then((response) => {
        response = response.body
        if (response.errno === ERR_OK) {
          this.seller = Object.assign({}, this.seller, response.data)
        }
      })
    },
    components: {
      'v-header': header
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7, 17, 27, 0.1))
      .tab-item
        flex: 1
        text-align: center
        color :rgb(250,20,20)
        .a
          display: block
          font-size: 14px
          color rgb(75,83,93)
          &.router-link-active
            color: rgb(240,20,20)



</style>
