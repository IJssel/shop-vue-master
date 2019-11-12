<template>
  <div class="home">
    <!-- 开头 -->
    <div class="flex-left">
      <div class="search-logo">
        <img src="../../images/menu1.png" alt="搜索" class="search-logo">
      </div> 
      <div class="search-ph" >
        <div class="inner">
          <i class="mintui mintui-search"></i> 
          <span>搜索商品</span>
        </div>
      </div>
    </div>

    <!-- 轮播图区域 -->
    <swiper :lunbotuList="lunbotuList" :isfull="true"></swiper>


    <!-- 九宫格 到 6宫格 的改造工程 -->
    <ul class="mui-table-view mui-grid-view mui-grid-9 grids-view">
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
        <router-link to="/home/newslist">
              <img src="../../images/icon1.png" alt="">
              <div class="mui-media-body">本地生活</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/home/photolist">
              <img src="../../images/icon2.png" alt="">
              <div class="mui-media-body">图片分享</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><router-link to="/home/goodslist">
              <img src="../../images/icon4.png" alt="">
              <div class="mui-media-body">商品购买</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
              <img src="../../images/icon3.png" alt="">
              <div class="mui-media-body">留言反馈</div></a></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
              <img src="../../images/icon5.png" alt="">
              <div class="mui-media-body">视频专区</div></a></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
              <img src="../../images/icon6.png" alt="">
              <div class="mui-media-body">美食</div></a></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
              <img src="../../images/icon7.png" alt="">
              <div class="mui-media-body">联系我们</div></a></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3"><a href="#">
            <img src="../../images/icon10.png" alt="">
            <div class="mui-media-body">更多</div></a></li>
    </ul> 

    <!--头条信息-->
    <div class="header-new">
      <span>头条助手：</span>
      <span>现在即未来:Samsung Galaxy Fold</span>
    </div>

    <!--商品列表-->
    <goodslist></goodslist>
    
  
  </div>
</template>

<script>
import { Toast } from "mint-ui";
import swiper from "../subcomponents/swiper.vue";
import goodslist from "../goods/GoodsList.vue";

export default {
  data() {
    return {
      lunbotuList: [] // 保存轮播图的数组
    };
  },
  created() {
    this.getLunbotu();
  },
  methods: {
    getLunbotu() {
      // 获取轮播图数据的方法
      this.$http.get("api/getlunbo").then(result => {
        // console.log(result.body);
        if (result.body.status === 0) {
          // 成功了
          this.lunbotuList = result.body.message;
        } else {
          // 失败的
          Toast("加载轮播图失败。。。");
        }
      });
    }
  },
  components: {
    swiper,goodslist
  }
};
</script>

<style lang="scss" scoped>
.home{
  background-color: #F1F1F1;
}
.flex-left{
    background: #fff;
   padding:10px;
   display: flex;
  .search-logo{
    width: 35px;
    img{
      height: 35px;
      // width: 30px;
    }
  }
}
.search-ph{
  background-color: #fff;
  padding: 5px;
  cursor: pointer;
  flex-basis: 0;
  flex-grow: 1;
  max-width: 100%;
  .inner{
    background-color: #e6e6e6;
    height: 35px;
    line-height: 20px;
    padding: 8px;
    border-radius: 14px;
    color: #999;
  }
}

.mui-grid-view.mui-grid-9 {
  background-color: #fff;
  border: none;
  border-radius: 2rem;
  margin:4px;
  img {
    width: 60px;
    height: 60px;
  }

  .mui-media-body {
    font-size: 13px;
  }
}

.mui-grid-view.mui-grid-9 .mui-table-view-cell {
  border: 0;
}

.header-new{
  height: 30px;
  width:95%;
  background-color: #fff;
  border-radius: 20px;
  padding:3px;
  margin:10px;
  span:first-child {
    color:red;
    font-weight: 600
  }
}
</style>
