<template>
  <div class="contain">
  <div class="user-info">
    <div class="user-img">
          <img src="../../images/me.jpg" alt="">
    </div> 
    <div class="info-unit">
        <h2 class="username">haohui</h2>
    </div>
  </div>
  
  <mt-cell title="我的订单" is-link to="/home"><span>查看全部</span></mt-cell>
  <ul class="mui-table-view mui-grid-view">
      <li class="mui-table-view-cell mui-media mui-col-xs-3">
        <router-link to="/home/newslist">
              <img src="../../images/daifukuan.png" alt="">
              <div class="mui-media-body">待付款</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-3"><router-link to="/home/photolist">
              <img src="../../images/daifahuo.png" alt="">
              <div class="mui-media-body">代发货</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-3"><router-link to="/home/goodslist">
              <img src="../../images/daishouhuo.png" alt="">
              <div class="mui-media-body">待收货</div></router-link></li>
      <li class="mui-table-view-cell mui-media mui-col-xs-3"><a href="#">
              <img src="../../images/tuikuan.png" alt="">
              <div class="mui-media-body">退款</div></a></li>
  </ul>
  <div class="items">
    <mt-cell class="item-cell" title="优惠券" is-link to="/home"></mt-cell>
    <mt-cell class="item-cell" title="地址管理" is-link to="/home"></mt-cell>
    <mt-cell class="item-cell" title="我的收藏" is-link to="/home"></mt-cell>
    <mt-cell class="item-cell" title="在线客服" is-link to="/home"></mt-cell>
  </div>





  </div>
</template>

<script>
</script>

<style lang="scss" scoped>
.contain{
    background-color: #fff;
    .user-info{
        display:flex;
        background-color:#ffff;
        padding: 20px 15px;
        align-items: center;
        // justify-content: center;
        .user-img{         
            img{
                height: 80px;
                display: block;
                border-radius: 100%;
            }
        }
        .info-unit{
            .username{
                padding-left: 15px;
                font-size: 20px;
                color: #ed662e;
                line-height: 24px;
                font-weight: 400;
            }
        }
    }
    .mui-grid-view{
        padding: 20px 0px;
        border: 0;
        li{
            padding: 5px;
            img{
                height: 30px;
            }
        }
    }
    .items{
        border:none;
        .item-cell{
        background-size: 120% 0px;
        }

    }
}
</style>
