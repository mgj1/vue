<template>
<div>

    <div class="header">
        <span class="fanhui" @click="prev()"><</span>
        <span class="title">支付页面</span>
    </div>
    <div class="list-content">
        <ul>
         <li class="food" v-for="(food, index) in cartFoods" :key="index">
            <span class="name">{{food.name}}</span>
            <div class="price"><span>￥{{food.price}}</span></div>
             <span class="fc">X{{food.count}}</span>
            
        </li>
      </ul>
    </div>
    <div class="content">
        <div class="content-left">
            <span class="total">待支付￥{{totalPrice}}</span>
        </div>
        <div class="content-right">
            <span class="pay" @click="order">确认支付</span>
        </div>
    </div>
</div>
</template>
<script>
import { mapState, mapGetters } from 'vuex';
import CartControl from '../../components/CartControl/CartControl.vue'
import localStore from '../../localStorage/localStorage.js'

    export default {
      data(){
        return{
          price:'',
          name:''
          //items:localStore.fetch(),
        }
      },
        components:{
        CartControl
        },
        computed: {
            ...mapState(['info', 'cartFoods']),
            ...mapGetters(['totalCount', 'totalPrice']),
        },
       // watch:{          
      // items:{
        //  handler:function(items){
         // localStore.save(items)   
      // },
       //  deep:true
      // }
  // },
        methods: {
            prev () {
            this.$router.go(-1)
           },
           order(){
             let comment=[]
             for(var i=0;i<this.cartFoods.length;i++){
               comment.push(this.cartFoods[i]);
             }
              localStorage.setItem('cmts',JSON.stringify(comment))
              localStorage.setItem('price',this.totalPrice)
              
            //console.log(this.comment)
             alert("下单成功")
             //localStorage.setItem('11','22')
             this.$store.dispatch('clearCart')
             this.$router.push({path:'/order'})
           }
        },

    }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
@import "../../common/stylus/mixins.styl"
  .header 
    height :50px
    width :100%
    background green
    .fanhui
      line-height 50px
      color :#fff
      font-size :20px
      margin-left :10px
    .title 
      line-height 50px
      font-size :20px
      margin-left :140px
      color :#fff
  .list-content
    margin-top :50px
    .food
      position relative
      padding 12px 0
      box-sizing border-box
      bottom-border-1px(rgba(7, 17, 27, 0.1))
      .name
        line-height 24px
        font-size 14px
        color rgb(7, 17, 27)
      .price
        position absolute
        right 50px
        bottom 12px
        line-height 24px
        font-size 14px
        font-weight 700
        color rgb(240, 20, 20)
      .fc
        position absolute
        right :150px
        bottom :12px
        line-height 24px
        font-size 14px
        font-weight 700
      .cartcontrol-wrapper
        position absolute
        right 0
        bottom 6px   
  .content  
    position fixed
    left 0
    bottom 0
    z-index 50
    width 100%
    height 48px
    background #141d27
    .content-left
      display :inline-block
      width :75%
      line-height :48px
      .total 
        margin-left :50px
        color :#ffffff
        font-size 15px
        font-weight 700
    .content-right 
      display :inline-block
      background :#00b43c
      width :23.5%
      line-height :48px
      .pay
        color :#ffffff
        font-size 15px
        font-weight 700
        margin-left :12px
         
</style>
