<template>
  <div id="shopcar">
    <div class="content">
      <div class="chart-wrapper">
        <div class="icon icon-shopping-cart" @click='isShow' :class="{have:totalCount !=0}"></div>
        <div class="total-count" v-show='totalCount !=0'>{{totalCount}}</div>
      </div>
      <div class="fee">
        <div class="total-fee" :class="{nowPrice:totalCount !=0}">￥{{totalPrice}}</div>
        <div class="deliverPrice">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="deliver-base" :class="{enough:totalPrice >= this.minPrice}">{{infoTotal}}</div>
    </div>
    <div class="foods-list-wrapper"  v-show="showList">
      <div class="gray" @click='isShow'></div>
      <div class="foods-list">
        <div class="list-title">
          <span class="foods-car">购物车</span>
          <span class="clear" @click="clear">清空</span>
        </div>
        <div class="list-content" v-for="(food,index) in selectFoods" :key="index">
          <span class="food-title">{{food.name}}</span>
          <countControl class="count-control" :foods="food"></countControl>
          <span class="food-price"><span class="rmb">￥</span>{{food.price}}</span>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import axios from "axios";
import countControl from './countControl'
export default {
  components:{
    countControl
  },
  name: "shopcar",
  props:{
    minPrice:{
      type : Number
    },
    deliveryPrice : {
      type : Number
    },
    selectFoods :{
      type : Array,
      default(){
        return []
      }
    },
  },
  data() {
    
    return {
      msg: {},
      fold : false
    };
  },
  created() {
    axios.get("/good/seller").then(res => {
      //   console.log(res)
    });
    this.fold = false
  },
  methods:{
    isShow(){
      // console.log(123)
      this.fold = !this.fold
    },
    clear(){
      this.selectFoods.forEach(item =>{
        item.count = 0
      })
    }
  },
  computed:{
    showList(){
      if(!this.totalCount){
        return false
      }else{
        if(this.fold == true){
          return true
        }
      }
    },
    totalCount(){
      let totalCount = 0;
      this.selectFoods.forEach((item) =>{
        totalCount += item.count
      })
      return totalCount
    },
    totalPrice(){
      let totalPrice = 0;
      this.selectFoods.forEach((item) =>{
        totalPrice += item.count * item.price
      })
      return totalPrice
    },
    infoTotal(){
      if(this.totalPrice === 0){
        return `￥${this.minPrice}`
      }else if(this.totalPrice > 0 && this.totalPrice < this.minPrice){
        let short = this.minPrice - this.totalPrice
        return `还差￥${short}起送`
      }else{
        return '去结算'
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
@import '../../static/style.css';
@import '../assets/stylus/index'

#shopcar 
  position: fixed;
  bottom: 0px;
  height: 48px;
  width: 100%;
  left: 0;

  .content 
    background-color: #141d27;
    display: flex;
    width 100%

    .chart-wrapper 
      flex: 0 0 80px;
      position relative
      .icon 
        font-size: 24px;
        line-height 44px
        text-align center
        vertical-align baseline
        color rgba(255,255,255,.4)
        position relative
        left 18px
        top -6px
        width 44px
        height 44px
        border-radius 44px
        border 6px solid #141d27
        background-color #2b333b
        &.have
          background-color #00a0dc
          color #ffffff
      .total-count
        position absolute
        right 0px
        top -6px
        width 24px 
        height 16px
        text-align center
        line-height 16px
        background-color rgb(240,20,20)
        box-shadow 0px 4px 8px 0px rgba(0,0,0,0.4)
        color #ffffff
        font-size 8px
        font-weight 700
        border-radius 16px


  
  .fee
    flex 1
    padding 12px 0 12px 12px
    height 24px
    .total-fee
      display inline-block
      line-height 24px
      color rgba(255,255,255,.2)
      font-size 16px
      font-weight 700
      border-1px-right(rgba(255,255,255,.4))
      padding-right 12px
      &.nowPrice
        color #ffffff
    .deliverPrice
      display inline-block
      font-size 12px
      padding-left 12px
      font-weight 700
      line-height 24px
      color rgba(255,255,255,.4)
  .deliver-base
    flex 0 0 105px
    font-size 12px
    line-height 48px
    color rgba(255,255,255,.1)
    font-weight 700
    background-color #2b333b
    // display inline-block
    text-align center
    padding 0 8px
    &.enough
      background-color green
      color #ffffff
.foods-list-wrapper
  position fixed
  top 0px
  bottom 48px
  width 100%
  display flex
  flex-direction column
  z-index -1
  .gray
    flex 1
    background-color rgba(7,17,27,0.6)
  .foods-list
    width 100%
    .list-title
      background-color #f3f5f7
      position relative
      padding 0 18px
      height 40px
      display flex
      justify-content space-between
      .foods-car
        font-size 14px
        font-weight 200
        color rgb(7,17,27)
        line-height 40px
       
      .clear
        font-size 12px
        color rgb(0,160,220)
        line-height 40px
    .list-content
      background-color #ffffff
      padding 12px 18px
      .food-title
        font-size 14px
        font-weight 200
        color rgb(7,17,27)
        line-height 24px
      .food-price
        float right 
        font-size 14px
        font-weight 700
        color rgb(240,20,20)
        line-height 24px 
        .rmb
          font-size 10px
      .count-control 
        float right 
        margin-left 12px
</style>



