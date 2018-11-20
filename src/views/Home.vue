<template>
  <div>
      <header class="nav-header">
        <div class="logo-wrap">
            <div class="logo-item">
                <img src="/static/huawei-logo.png">
            </div>
        </div>
        <div class="search-wrap" @click="toSearch">
            <div class="search-item">
                <i class="icon iconfont icon-sousuo ico-search"></i>
                搜索商品名称
            </div>
        </div>
        <div class="user-wrap">
            <div class="user-item">
                <div @click="open('/user')"><i class="icon iconfont icon icon-wo ico-user"></i></div>
            </div>
        </div>
    </header>

    <section class="content-wrap">
        <!-- 轮播图 -->
        <div class="banner-wrap">
            <mt-swipe :auto="4000">
                <mt-swipe-item><router-link to="/goodsdetail?id=0003"><img src="https://res.vmallres.com/pimages//sale/2018-10/20181031231452878.png" alt="华为"></router-link></mt-swipe-item>
                <mt-swipe-item><router-link to="/goodsdetail?id=0002"><img src="https://res.vmallres.com/pimages//sale/2018-11/20181101141551906.png" alt="华为Note5"></router-link></mt-swipe-item>
            </mt-swipe>
        </div>
        <!-- 内容区导航栏 -->
        <ul class="nav-list">
            <li class="list-item">
                <a href="">
                    <img src="https://res.vmallres.com/pimages//squaredInfo/icon/20181101/4bc22bc02a152ee53a6ebadf07952172.png" alt="">
                    <div class="img-nav">优选配件</div>
                </a>
                
            </li>
            <li class="list-item">
                <a href="">
                    <img src="https://res.vmallres.com/pimages//squaredInfo/icon/20181101/9e8d0f831507a3fe550789ea96c72e68.png" alt="">
                    <div class="img-nav">邀请有礼</div>
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="https://res.vmallres.com/pimages//squaredInfo/icon/20181101/3c303e2e34d78162fd73f106ee4dadf2.png" alt="">
                    <div class="img-nav">会员领券</div>
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="https://res.vmallres.com/pimages//squaredInfo/icon/20181101/0e73ad800ed1de96f404436291feeb93.png" alt="">
                    <div class="img-nav">以旧换新</div>
                </a>
            </li>
            <li class="list-item">
                <a href="">
                    <img src="https://res.vmallres.com/pimages//squaredInfo/icon/20181101/e786f27e9788b2546accbdfa70cd3621.png" alt="">
                    <div class="img-nav">优购码</div>
                </a>
            </li>
        </ul>
        <!-- 商品列表区 -->
        <div class="goods-wrap">
            <!-- 大图区 -->
            <ul class="big-item-list">
                <li class="big-item"><router-link to="/goodsdetail?id=0012">
                    <div class="youhui">超值优惠</div>
                    <img src="https://res.vmallres.com/pimages///cop/20180928120612859/1538107572859.jpg" alt="">
                </router-link>
                </li>
                <li class="big-item">
                    <div class="youhui">为你推荐</div>
                    <router-link to="/goodsdetail?id=0013">
                    <img src="https://res.vmallres.com/pimages///cop/20171220152704237/1513754824237.jpg" alt="">
                    </router-link>
                </li>
            </ul>
            <!-- 小图区 -->
            <ul class="normal-item-list clearfix">
                <li class="normal-item" v-for="item in goodsList" @click="viewGoods(item.goodsId)">
                    <div class="img">
                        <img :src="item.goodsImg" alt="">
                    </div>
                    <div class="info">
                        <div class="name">{{item.goodsName}}</div>
                        <div class="brief">{{item.goodsBrief}}</div>
                        <div class="price">
                            ￥{{item.goodsPrice}}
                        </div>
                    </div>
                </li>
            </ul>
        </div>
    </section>

    <!-- <nav-footer></nav-footer> -->
  </div>
</template>

<script>
import '@/assets/css/reset.css'
import '@/assets/css/homepage.css'
import {Swipe,SwipeItem} from 'mint-ui'
import axios from 'axios'
export default {
  data(){
      return {
          goodsList: []
      }
  },
  methods: {
     init(){//获取数据
        axios.get('/static/mock/Home.json').then(result=>{
            var goodsData = result.data;
            //console.log(goodsData);
            this.goodsList = goodsData.goodsList;
        });
     },
     viewGoods(goodsId){
         this.$router.push({
             path:"goodsdetail",
             query:{id: goodsId}
         });
     },
     toSearch(){
         this.$router.push({
             path: 'search'
         });
     },
     open(path){
         this.$router.push({
             path: path
         });
     } 
  },
  created:function(){
      this.init();
  }
}
</script>

<style>
    .banner-wrap{
        height: 8rem;
    }
    .banner-wrap img{
        width: 100%;
        height: 8rem;
    }
</style>

