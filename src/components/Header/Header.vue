<template lang="html">
      <header>
        <!-- 商家信息 -->
        <div class="seller">
            <img :src="seller.avatar" alt="">
            <div class="sellerinfo">
                <h2><span></span>{{seller.name}}</h2>
                <p class='delivery'>{{seller.description}}/{{seller.deliveryTime}}分钟送达</p>
                <p class="pay">{{seller.supports[0].description}}</p>
            </div>
            <div class="button" @click="show=true">5个 ></div>
        </div>
        <!-- 公告 -->
        <div class="notice" @click="show=true">
          <span></span>
          <p>{{seller.bulletin}}</p>
          <i> > </i>
        </div>
        <!-- 背景层 -->
        <div class="bg"><img :src="seller.avatar" alt=""></div>
        <!-- 弹出层 -->
        <transition name='pop'>
            <my-pop :seller='seller' v-show="show" @close="show=false"></my-pop>
        </transition>


      </header>
</template>

<script>
import Pop from "../Pop/Pop"
export default {
  data(){
    return{
      show:false,
    }
  },
  props:{
    seller:{
      type:Object,
      required:true
    },
  },
  components:{
    "my-pop":Pop,
  }
}
</script>

<style lang="less" scoped>
  .pop-enter-active{animation: pop-in 0.5s};
  .pop-leave-active{animation: pop-out 0.5s};
  @keyframes pop-in{
    0%{transform: scale(0)};
    50%{transform: scale(1.5)};
    100%{transform: scale(1)}
  };
  @keyframes pop-out{
    0%{transform: scale(1)};
    50%{transform: scale(1.5)};
    100%{transform: scale(0)}
  };
  header{
    height:134px;
    .seller{
      display:flex;
      padding:24px 12px 18px 24px;
      color:rgb(255,255,255);
      img{
        width:64px;
        height:64px;
        margin-right:16px;
        font-weight:200;
      }
      .sellerinfo{
        height:64px;
        display:flex;
        flex-grow: 1;
        flex-direction: column;
        justify-content:space-between;
        h2{
          font-size:16px;
          font-weight:bold;
          line-height:18px;
          span{
            width: 30px;
            height: 18px;
            display: inline-block;
            background: url('./brand@2x.png') no-repeat;
            background-size: contain;
            vertical-align: middle;
            margin-right: 5px;
          }
        }
        .delivery{
          font-size: 12px;
          line-height:12px;
        }
        .pay{
          font-size: 10px;
          line-height:12px;
        }
      }
      .button{
        font-size:10px;
        height:20px;
        border-radius: 8px 7px;
        background-color: rgba(0,0,0,.2);
        padding: 10px 15px;
        align-self: flex-end;
        line-height: 20px;

      }
    }
    .bg{
      position:absolute;
      width:100%;
      height:134px;
      z-index:-1;
      left:0;
      top:0;
      overflow: hidden;
      filter:blur(5px);
      img{
        width:100%;
      }
    }
    .notice{
      padding:0 12px;
      display:flex;
      height:28px;
      background-color: rgba(7,17,27,.2);
      font-size:10px;
      color:rgb(255,255,255);
      font-weight: 200;
      line-height:28px;
      span{
        background: url(./bulletin@2x.png) no-repeat;
        min-width:22px;
        min-height:12px;
        background-size: contain;
        background-position: center;
        margin-right:4px;
      }
      p{
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }
    }
  }
</style>
