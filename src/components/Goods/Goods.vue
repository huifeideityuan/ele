<template lang="html">
  <div class="">
    <div class="goods">
      <div class="menu" id='menu'>
        <ul>
          <!-- <li v-for="(item,index) in goods " :key='index' @click="selectCategory(index)" :class="{active:index==current}"> -->
          <li v-for="(item,index) in goods" :key="index" :class="{active:index===current}"  @click="selectCategory(index)"  >
            <div class="">
              {{item.name}}
            </div>
          </li>
        </ul>
      </div>
      <div class="list" id='list'>
        <div class="" ref='list'>
          <dl v-for="(item,index) in goods" :key='index'>
            <dt>{{item.name}}</dt>
            <dd v-for='(food,idx) in item.foods' @click="sendFood(food)" >
              <img :src="food.icon" alt="">
              <div class="">
                <h2>{{food.name}}</h2>
                <p v-if='food.description' class='description'>{{food.description}}</p>
                <p>月售{{food.sellCount}}份  好评率{{food.rating}}%</p>
                <p class='price'><strong><span>¥</span>{{food.price}}</strong><del v-show='food.oldPrice'><span>¥</span>{{food.oldPrice}}</del></p>

                  <div class="myaddfood">
                    <my-addfood :food='food'></my-addfood>
                  </div>

              </div>

            </dd>
          </dl>
        </div>
      </div>
    </div>

    <transition name='slide'>
      <div class="food-info" v-if='show'>
        <my-food  :foodinfo= 'currentFood'  @close="close"></my-food>
      </div>
    </transition>
    <my-cart :cartgoods='cartGoods'></my-cart>
  </div>
</template>

<script>
  const shop=require('../../api/data.json')
  import IScroll from '../../../static/js/iscroll-probe'
  import Food from '../Food/Food-1'
  import AddFood from '../AddFood/AddFood'
  import Cart from '../Cart/Cart'
    export default {
      data(){
        return{
          goods:[],
          current:0,
          listHeight:[0],
          currentFood:{},
          show:false,
          seller:[]
        }
      },
      components:{
        'my-food':Food,
        'my-addfood':AddFood,
        'my-cart':Cart

      },
      methods:{
        selectCategory(index){
          console.info('aaa')
            this.current = index;
            //获取所有的dl
            // let dls = this.$refs.list.getElementsByTagName('dl');
            let dls=this.$refs.list.getElementsByTagName('dl');
            this.scrolllist.scrollToElement(dls[this.current]);
            // //调用scrollToElement方法
            // this.listScroll.scrollToElement(dls[this.current]);
        },
        getlistHeight(){
          let dls=this.$refs.list.getElementsByTagName('dl');
          for(let i=0;i<dls.length;i++){
            this.listHeight.push(dls[i].clientHeight+this.listHeight[i])
          }
          // console.info('bbb')
          // console.info(this.listHeight)
        },
        sendFood(food){
          this.currentFood=food;
          this.show=true;
          console.log(this.show);
          console.dir(this.currentFood)
        },
        close(){
          this.show=false;
        }
      },
      computed:{
        cartGoods(){
          let cartgoods=[];
          for( let i=0; i<this.goods.length; i++){
            if(this.goods[i].count){
              cartGoods.push(goods[i]);
            }
          }
          return cartgoods;
        }
      },
      created(){
        this.goods=shop.goods;
        this.seller=shop.seller
      },
      mounted(){
        new IScroll('#menu');
        this.scrolllist=new IScroll('#list',{probeType:2});
        this.getlistHeight();
        let that=this;
        this.scrolllist.on('scroll',function(){
          // console.log(this.y)
            let dis=Math.abs(this.y);
            for( let i=0;i<that.listHeight.length;i++){
              if(dis>that.listHeight[i] && dis<that.listHeight[i+1]){
                that.current=i;
              }
            }


        })

      },
    }
    </script>

<style lang="less" scoped>
  .slide-enter, .slide-leave-active{transform:translateX(100%);opacity:0}
  .slide-enter-active , .slide-leave-active {transition:all 1s}
  .goods{
    display:flex;
    position:fixed;
    top:174px;
    left:0;
    bottom:48px;
    right:0;
    overflow: hidden;
    .menu{
      width:80px;
      font-size:12px;
      background-color: #f3f5f7;
      color:rgb(77,85,93);
      li{
        // padding:0 12px;
        &.active{
          background-color: #fff;
          div{
            border-bottom:none;
          }
        }
        div{
          height:54px;
          width:56px;
          margin-left:12px;
          margin-right:12px;
          border-bottom:1px solid rgba(7,17,27,.1);
          display: flex;
          align-items: center;
        }
      }

    }
    .list{
      flex-grow: 1;
      dt{
        border-left:3px solid #D9DDE1;
        padding-left: 14px;
        height:26px;
        line-height: 26px;
        font-size: 12px;
        color:rgb(147,153,159);
        background-color: #f3f5f7;
      }
      dd{
        padding:18px;
        display:flex;
        position:relative;
        img{
          width:57px;
          height:57px;
          border-radius: 2px;
        }
        div{
            flex-grow: 1;
            margin-left: 10px;
          h2{
            font-size: 14px;
            color:rgb(7,17,27);
            line-height: 14px;
          }
          p{
            width:190px;
            font-size: 10px;
            height:12px;
            color:rgb(147,153,159);
            line-height: 12px;
            margin-top:8px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
          }
          p.price{
            overflow: visible;
            strong{
              font-size: 14px;
              color:rgb(240,20,20);
              line-height:24px;
              font-weight: 700;
              margin-right:8px;
              span{
                font-weight: normal;
                font-size: 10px;
              }
              del{
                font-size: 10px;
                color:rgb(147,15,159);
                height:24px;
                line-height: 24px;
                font-weight: 700;
                span{
                  font-weight: normal;
                }
              }
            }
          }
          .myaddfood{
            position:absolute;
            right:18px;
            bottom:0;
            width:72px;

          }
        }
      }
    }

  }

</style>
