<template>
  <div>
    <section class="order">
      <HeaderTop title="订单列表"></HeaderTop>
      <section class="order_no_login" v-show="isShow" v-model="show">
        <!--<img src="./images/order/person.png">-->
        <h3>登录后查看外卖订单</h3>
        <button @click="denglu">立即登陆</button>
      </section>
    </section>
    <div class="orderlist" v-show="!isShow&&price>0" v-model="shuju">
      <div class="order1">
       <img class="img1" width="50" height="50" src="http://p1.so.qhimgs1.com/sdr/400__/t014467d9a5a452fa5d.jpg">
       <span class="span1">广东海洋大学></span>
       <span class="span2">订单已完成</span>
      </div>
      <div class="order2">
        <ul>
          <li class="food" v-for="(food, index) in list" :key="index">
            <span class="span3">{{food.name}}</span>
          </li>
        </ul>
        <span class="span4">￥{{price}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import HeaderTop from '../../components/HeaderTop/HeaderTop.vue'
import {mapState, mapGetters} from 'vuex'
import CartControl from '../../components/CartControl/CartControl.vue'
export default {
  data () {
    return {
      isShow: true,
      list:[],
      price:''
    }
  },
  components: {
    HeaderTop,
    CartControl
  },
  computed:{
    ...mapState(['info', 'cartFoods','userInfo']),
    ...mapGetters(['totalCount', 'totalPrice']),
    show(){
      if(this.userInfo.name){
        this.isShow=!this.isShow
      }
    },
    shuju(){
      let list = JSON.parse(localStorage.getItem('cmts') || "[]")
      let price =localStorage.getItem('price')
      this.price=price
      this.list = list
      //console.log(this.list)
    }
  },
  methods:{
    
    denglu(){
        this.$router.push({path:'/Login'})
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixins.styl"
  .order  //订单
    width 100%
    .order_no_login
      padding-top 140px
      width 60%
      margin 0 auto
      text-align center
      >h3
        padding 10px 0
        font-size 17px
        color #6a6a6a
      >button
        display inline-block
        background #02a774
        font-size 14px
        color #fff
        border 0
        outline none
        border-radius 5px
        padding 10px 20px
  .orderlist
    margin-top:45px
    background :#fff
    .order1
      width 100%
      height 70px
      position relative
      bottom-border-1px(rgba(7, 17, 27, 0.1))
      .img1
        padding :10px
      .span1
        position absolute
        top:12px 
        left :70px
        color :#323130
        font-size :17px
      .span2
        position:absolute
        top:12px
        right:2px
        font-size :13px
        color :#16130f
    .order2
      width 100%
      height 70px
      position relative
      .food
        float left
        margin-top:20px
        font-size :14px
        margin-left :5px
      .span4
        position:absolute
        top:20px
        right:2px
        color :#f8273b

</style>
