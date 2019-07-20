<template>
    <div>
        <div class="header">
        <span class="fanhui" @click="prev()"><</span>
        </div>
        <div class="footer">
        <shop-list></shop-list>
        </div>
    </div>
</template>
<script>
import { mapState } from 'vuex'
import Star from "../../components/Star/Star.vue"
import ShopList from "../../components/ShopList/ShopList.vue"
export default {
    data(){
        return {//elm.cangdu.org/img/
            baseImgUrl: 'http://'
        }
    },
    components: {
        Star,
        ShopList
    },
    computed: {
        ...mapState(['shops'])
    },
    methods: {
      prev () {
      this.$router.go(-1)
      }
    }
}
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
    @import "../../common/stylus/mixins.styl"
.header 
  width :100%
  height :50px
  .fanhui 
    font-size :20PX
    font-weight :700
    color :green
    line-height 50px
    margin-left :5px
.footer 
 margin-top :50px

</style>
