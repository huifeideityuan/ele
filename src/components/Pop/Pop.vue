<template lang="html">
    <div class="pop">
        <h2>{{seller.name}}</h2>
        <div class="preferential">
          <h3>优惠信息</h3>
          <ul>
            <li v-for='(item,index) in seller.supports'>{{item.description}}</li>
          </ul>
        </div>
        <div class="notice">
          <h3>商家公告</h3>
          <div class="">
            {{seller.bulletin}}
          </div>
        </div>
        <div class="close"@click="close">x</div>
    </div>
</template>

<script>
export default {
  methods:{
    close(){
      this.$emit("close")
    },
  },
  props:{
    seller:{
      type:Object,
      required:true
    }
  }
}
</script>

<style lang="less" scoped>
  .pop{
    position:fixed;
    padding:64px 48px 32px;
    top:0;
    left:0;
    right:0;
    bottom:0;
    z-index:1;
    background-color: rgba(7,17,27,.8);
    color:rgb(255,255,255);
    h2{
      margin:0 auto 68px;
      text-align: center;
      font-size:16px;
      font-weight:700;
      line-height: 16px;
    }
    .preferential{
      h3{
        font-size:14px;
        font-weight:700;
        line-height: 14px;
        text-align: center;
        margin-bottom:24px;
      }
      ul{
        font-size:12px;
        font-weight:200;
        line-height: 24px;
      }

    }
     .notice{
       margin-top:28px;
          h3{
            font-size:14px;
            font-weight:700;
            line-height: 14px;
            text-align: center;
            margin-bottom:24px;
          }
          div{
            font-size:12px;
            font-weight:200;
            line-height: 24px;
          }

        }
    .close{
      font-size: 32px;
      color:rgba(0,0,0,.5);
      position:absolute;
      bottom:32px;
      left:50%;
      transform: translateX(-50%);
    }
  }
</style>
