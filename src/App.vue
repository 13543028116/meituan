<template>
  <div id="app">
    <!-- 头部 -->
    <app-header :poiInfo="poiInfo">

    </app-header>

    <!-- 导航 -->
    <app-nav :commentNum="commentNum">
      
    </app-nav>

    <!-- 内容 -->
    <!-- <keep-alive>保留页面请求 -->
    <keep-alive>
      <router-view>
        
      </router-view>
    </keep-alive>
  </div>
</template>

<script>
import Header from './components/header/Header'
import Nav from './components/nav/Nav'

export default {
  name: 'App',
  components: {
    "app-header":Header,
    "app-nav":Nav
  },
  // api接口传值
  data(){
    return{
      poiInfo:{},
      commentNum:0
    }
  },
  created(){
      //请求goods结果 
      fetch("/api/goods")
       .then(res =>{
        //  数据转换
         return res.json()
       })
       .then(Response =>{
        //  console.log(Response)
        if(Response.code == 0){
          this.poiInfo = Response.data.poi_info
          
        }
       })
      //请求ratings
      fetch("/api/ratings")
       .then(res =>{
        //  数据转换
         return res.json()
       })
       .then(Response =>{
        //  console.log(Response)
        if(Response.code == 0){
          this.commentNum = Response.data.comment_num
          
        }
       })  
  }
}
</script>

<style>

</style>
