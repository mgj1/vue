<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="iconfont icon-removecircleoutline" v-if="food.count" @click.stop="updateFoodCount(false)"></div>
    </transition>
    <div class="cart-count" v-if="food.count">{{food.count}}</div>
    <div class="iconfont icon-addcircle" @click.stop="updateFoodCount(true)"></div>
  </div>
</template>

<script>
import {mapState} from 'vuex'
import { MessageBox } from 'mint-ui'
export default {
  props: {
    food: Object
  },
  computed: {
    ...mapState(['userInfo'])
  },
  methods: {
    updateFoodCount (isAdd) {
      if(!this.userInfo.name){
        MessageBox.confirm('您还没有登陆，是否要登陆？').then(
        action => {
          // 请求退出
          //this.$store.dispatch('updateFoodCount')
          //Toast('退出成功')
          this.$router.push({path:'/Login'})
        },
        action => {
          //console.log('取消登录')
        }
      )
        return;

      }
      //console.log(this.userInfo.name)
      this.$store.dispatch('updateFoodCount', {isAdd, food: this.food})
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixins.styl"
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)

    .icon-removecircleoutline
      display: inline-block
      padding 6px
      line-height 24px
      font-size 24px
      color $green
      &.move-enter-active, &.move-leave-active
        transition all .3s
      &.move-enter, &.move-leave-to
        opacity 0
        transform translateX(15px) rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .icon-addcircle
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color $green
</style>
