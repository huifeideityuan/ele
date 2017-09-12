<template lang="html">
  <div class="addfood">
    <transition name="roll" >
        <div class="sub" v-show='food.count'@click.stop="subcount">
            <i class='iconfont icon-jian' ></i>
        </div>
    </transition>


    <div class="count" v-show='food.count'>{{food.count}}</div>
    <transition name="fade" >
        <div class="add" @click.stop="addcount">
            <i class='iconfont icon-jia'></i>
        </div>
    </transition>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    food:{
      type:Object,
      required:true
    }
  },
  data(){
    return{
      // currentcount:0,
    }
  },
  methods:{
    addcount(){
      if(this.food.count){
        this.food.count++;
        // this.currentcount=this.food.count;
      }else{
        this.$set(this.food,"count",1);
        // this.currentcount=this.food.count;
      }
    },
    subcount(){
      if(this.food.count>0){
        this.food.count--;
        // this.currentcount=this.food.count;
      }
    }
  }
}
</script>

<style lang="less" scoped >
// .roll-enter,.roll-enter-active{transfrom:translateX(200%) rotateZ(360deg);}
// .roll-enter-active,.roll-leave-active{transition:all 1s}
// .fade-enter,.fade-enter-active{opacity:0}
// .fade-enter-active,.fade-leave-active{transition:all 1s}
.roll-enter,.roll-leave-active{transform: translateX(200%) rotateZ(360deg);}
.roll-enter-active,.roll-leave-active{transition: all 1s;}
.fade-enter,.fade-leave-active{opacity: 0;}
.fade-enter-active,.fade-leave-active{transition: all 1s;}
  @import '../../assets/css/font.css';
  .addfood{
    width:72px;
    height:24px;
    position:relative;
            text-align: center;
      .sub{
        width:24px;
        height:24px;
        color:rgb(0,160,220);
        font-size:24px;
        line-height:24px;
        position:absolute;
        top:-2px;
        left:0;
      }
      .count{
        position:absolute;
        top:0;
        left:24px;
        color:rgb(147,153,159);
        font-size:10px;
        width:24px;
        height:24px;
        line-height:24px;

      }
      .add{
        font-size:24px;
        color:rgb(0,160,220);
        line-height:24px;
        position:absolute;
        top:0;
        right:0;
        width:24px;
        height:24px;
        line-height:24px;
      }
  }
</style>
