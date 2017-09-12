<template>
  <div id="app">
    <my-header :seller="seller"></my-header>
      <ul class='nav'>
        <li><router-link to="/">商品</router-link></li>
        <li><router-link to="/ratings">评论</router-link></li>
        <li><router-link to="/seller">商家</router-link></li>
      </ul>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from "./components/Header/Header"
const shop = require("./api/data.json")
export default {
  name: 'app',
  data(){
    return{
      seller:{}
    }
  },
  components:{
    'my-header':Header
  },
  created(){
    this.seller=shop.seller
  }
}
</script>

<style lang='less' scoped>
    .nav{
        height:40px;
        display:flex;
        justify-content: space-around;
        border-bottom: 1px solid rgb(7,17,27,.1);
      a{
        font-size: 14px;
        color:rgb(77,85,93);
        line-height:40px;
        text-decoration:none;
        &.router-link-exact-active{
          color:rgb(240,20,20);
        }
      }
    }
</style>
