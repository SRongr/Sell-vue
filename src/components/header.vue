<template>
  <div class="header backg">
    <div class="content-wrapper">
      <div class="avatar">
        <img :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <div class="content-title">
          <span class="brand"></span>
          <span>{{seller.name}}</span>
        </div>
        <div class="content-middle">
          {{seller.description}}/{{seller.deliveryTime}}分钟送达
        </div>
        <div class="supports" v-if="seller.supports">
          <span class="icon" :class="decMap[seller.supports[0].type]" ></span>
          <span>{{seller.supports[0].description}}</span>
        </div>
        <div class="number-wrapper" v-if='seller.supports'>
          <span class="number">{{seller.supports.length}}个</span>
          <span class="icon-cheveron-right more"></span>
        </div>
      </div>
   </div>
   <div class="bulletin-wrapper">
     <span class="bulletin"></span><span class="text">{{seller.bulletin}}</span>
     <span class="icon-cheveron-right more"></span>
   </div>
   <div class="background">
     <img :src="seller.avatar" alt="">
   </div>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  props:{
    seller:{
      type : Object
    }
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  created() {
    this.decMap = ['decrease','discount','special','invoice','guarantee']
    console.log(this.seller)
    
    var timer = setTimeout(()=>{
    console.log(113)
    console.log(this)
    console.log(this.seller)
    console.log(this.seller.score)
    },1500)
    // console.log(113)
    // console.log(this)
    // console.log(this.props)
    // console.log(this.$seller)
    // console.log(seller)
    // console.log(this.seller.score)
  }
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
@import '../../static/style.css'
@import '../assets/stylus/index.styl'
// @import '../assets/svg/style.css'
  .header
    position relative
    font-size 0
    overflow hidden
    .content-wrapper
      position relative
      padding 24px 24px 18px
      background-color rgba(7,17,27,0.5)
      .avatar
        float left
        img
          border-radius 2px 
          set-img(64px)
      .content
        margin-left 64px
        padding 2px 0 2px 16px
        .content-title
          font-size 16px
          color rgb(255,255,255)
          font-weight bold
          line-height 18px
          .brand
            display inline-block
            bg-image('brand')
            width 30px
            height 18px
            background-size 30px 18px
            vertical-align top
            
        .content-middle
          padding-top 8px
          font-size 12px
          color #ffffff
          font-weight 200
          line-height 12px
        .supports
          margin-top 10px
          font-size 10px
          color rgb(255,255,255)
          font-weight 200
          line-height 13px
          .icon
            display inline-block
            vertical-align top
            width 14px 
            height 14px
            background-size 14px 14px
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
            
        
        .number-wrapper
          position absolute
          right 12px
          bottom 11px
          padding 7px 8px
          background-color rgba(0,0,0,0.2)
          border-radius 16px
          font-size 10px 
          color rgb(255,255,255)
          font-weight 200
          line-height 12px
          .number
          .more
            width 2px
            vertical-align middle
    .bulletin-wrapper
      position relative
      font-size 10px 
      background-color rgba(7,17,27,0.2)
      font-weight 200 
      height 28px
      line-height 28px
      padding 0 18px 0px 12px
      white-space nowrap
      overflow hidden
      text-overflow ellipsis
      color rgb(255,255,255)
      .bulletin 
        width 22px 
        height 12px
        display inline-block
        bg-image('bulletin')    
        background-size 22px 12px 
        vertical-align middle
      .text
        margin-left  4px
        font-size 10px 
        vertical-align top 
      .more
        font-size 10px 
        position absolute
        right 12px
        bottom 8px
        margin-left 4px
    .background
      position absolute
      top 0
      left 0
      z-index -1
      width 100%
      img 
        background-size cover
        width 100%
        
            

          
</style>