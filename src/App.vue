<template>
  <div id="app">
    <!-- <div class="header">header</div> -->
    <v-header :seller = 'seller'></v-header>
    <div class="tab border-1px">
      <div class="tab-item"><router-link to='goods'>商品</router-link></div>
      <div class="tab-item"><router-link to='ratings'>评价</router-link></div>
      <div class="tab-item"><router-link to='sellers'>商家</router-link></div>
    </div>
    <div class="content">
      <router-view :seller="seller"></router-view>
    </div>
  </div>
</template>

<script>
import header from './components/header'
import goods from './components/goods'
import axios from 'axios'
// import sellers from './components/ratings'
export default {
  name: 'App',
  data (){
    return {
      msg:'asd',
      seller:{},
      obj:{
        aa:123132,
        bb:45646,
        aaa:123132,
        bbb:45646,
        aasdb:123132,
        bba:45646,
        aaads:123132,
        basdab:45646,
        adasa:123132,
        basddab:45646,adasdasa:123132,
        basdb:45646,aa:123132,
        asdbb:45646,aasdasdassdaa:123132,
        basdb:45646,
      }
    }
  },
  components:{
    'v-header' : header,
    goods,
   
  },
  created(){
    console.log(this)
    var timer = setTimeout(()=>{
      console.log(123)
    },5000)
    axios.get('/good/seller').then(
      res => {
        // console.log(res)
        if(res.data.code === 0){
          this.seller = res.data.data

          console.log(this.seller)
        }
      }
    )
    console.log(this.seller)
  }
}
</script>


<style lang="stylus" ref='stylesheet/stylus'>
@import 'assets/stylus/index.styl'
 #app
   .tab
     display flex
     height 40px
     line-height 40px
     border-1px(rgba(240,20,20,0.1))
    .tab-item
      flex 1
      text-align center
      font-size 14px;
      color rgb(77,85,93)
      a
        width 100%
        height 100%
        display block
      a.active
        color : rgb(240,20,20)!important
</style>

