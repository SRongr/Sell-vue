<template>
  <div id="countControl">
    <span class="decrease icon-minus-outline" v-show="foods.count > 0" @click="decreaseFoods"></span>
    <span class="count" v-show="foods.count > 0">{{foods.count}}</span>
    <span class="increase icon-add-solid" @click="increaseFoods"></span>
  </div>
</template>

<script>
import axios from 'axios'
import Vue from 'vue'
export default {
  props : {
    foods : {
      type : Object

    }
  },
  data () {
    return {
    //  foods:{

    //  }
    }
  },
  methods:{
    increaseFoods(e){
      if(e._constructed){    //走scroll 的click 事件
        if(!this.foods.count){
          Vue.set(this.foods,'count')   //vue提供的方法 设置对象的属性  添加一个属性
          this.foods.count = 1
        }else{
          this.foods.count ++
        }
      }else{
        this.foods.count ++
      }
    },
    decreaseFoods(e){
      if(e._constructed){
        if(this.foods.count === 0){
          return
        }else{
          this.foods.count --
        }
      }else{
        this.foods.count --
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" scoped>
@import '../../static/style.css'; 
  #countControl
    // background-color #000
    font-size 0px
    .decrease, .increase
      font-size 24px
      color rgb(0,160,220)
      padding 6px
     display inline-block
    .count
      font-size 10px
      color rgb(147,153,159)
      line-height 24px
      display inline-block
      width 12px
      text-align center
      vertical-align top

      
</style>
