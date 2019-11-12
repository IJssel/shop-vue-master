<template>
  <div class="shopcar-container">
    <!-- 开头 -->
    <mt-header title="购物车" class="shop-header">
      <router-link to="/" slot="left">
        <mt-button icon="back">返回</mt-button>
      </router-link>
      <mt-button slot="right">删除</mt-button>
    </mt-header>

    <!-- 商品列表项区域 -->
    <div class="goods-list">
      <div v-infinite-scroll="loadMore" infinite-scroll-disabled="loading" infinite-scroll-distance="10">
          <div v-for="item in goodslist" :key="item.id">
            <div class="mui-card-content-inner">
              <mt-checklist v-model="$store.getters.getGoodsSelected[item.id]" :options="['']" @change="selectedChanged(item.id, $store.getters.getGoodsSelected[item.id])" class="mt-checklist"> </mt-checklist>  

              <img :src="item.thumb_path">
              <div class="info">
                <h>{{ item.title }}</h>
                <div>
                  <span class="price">￥{{ item.sell_price }}</span>
                  <numbox :initcount="$store.getters.getGoodsCount[item.id]" :goodsid="item.id" class="info-numbox"></numbox>
                </div>
                  <!-- <a href="#" @click.prevent="remove(item.id, i)">删除</a> -->
              </div>

          </div>
          </div>
        </div>
    </div>

    <!-- 结算区域 -->
    <div class="cartfooter">
        <div class="left">
          <p>总计（不含运费）</p>
          <p><span class="red">{{ $store.getters.getGoodsCountAndAmount.count }}</span> 件，合计<span class="red">￥{{ $store.getters.getGoodsCountAndAmount.amount }}</span></p>
        </div>
          <mt-button type="danger" class="right">去结算</mt-button>
    </div>

    <!-- 猜你喜欢 -->
    <div class="he-similar">
      <div class="he-title">猜你喜欢</div>
    </div>



  </div>
</template>

<script>
import numbox from "../subcomponents/shopcar_numbox.vue";

export default {
  data() {
    return {
      goodslist: [] // 购物车中所有商品的数据
    };
  },
  created() {
    this.getGoodsList();
  },
  methods: {
    getGoodsList() {
      // 1. 获取到 store 中所有的商品的Id，然后拼接出一个 用逗号分隔的 字符串
      var idArr = [];
      this.$store.state.car.forEach(item => idArr.push(item.id));
      // 如果 购物车中没有商品，则直接返回，不需要请求数据接口，否则会报错
      if (idArr.length <= 0) {
        return;
      }
      // 获取购物车商品列表
      this.$http
        .get("api/goods/getshopcarlist/" + idArr.join(","))
        .then(result => {
          if (result.body.status === 0) {
            this.goodslist = result.body.message;
          }
        });
    },
    remove(id, index) {
      // 点击删除，把商品从 store 中根据 传递的 Id 删除，同时，把 当前组件中的 goodslist 中，对应要删除的那个商品，使用 index 来删除
      this.goodslist.splice(index, 1);
      this.$store.commit("removeFormCar", id);
    },
    selectedChanged(id, val) {
      // 每当点击开关，把最新的 快关状态，同步到 store 中
      // console.log(id + " --- " + val);
      this.$store.commit("updateGoodsSelected", { id, selected: val });
    }
  },
  components: {
    numbox
  }
};
</script>

<style lang="scss" scoped>
.shopcar-container {
  overflow: hidden;

  .shop-header{
    background-color: #fff;
    color: black;
    font-size: 16px;
    font-weight: 600;
  }

  .goods-list {
    .mui-card-content-inner {
      display: flex;
      align-items: center;
      .mt-checklist{
        // border: none;
        // width: 40px;
        /deep/ a{
          background-size: 120% 0px;
          .mint-cell-wrapper{
            // background-color: red;
            background-size: 120% 0px;
            padding: 0;
            .mint-checklist-label{
              padding:0;
              .mint-checkbox-input:checked + .mint-checkbox-core{
                background-color: #ed662e;
                border-color: #ed662e;
              }
            }
          }
        }
      }
     
    }
    img {
      width: 64px;
    }
    h {
      font-size: 12px;
    }
    .info {
      padding-left: 10px;
      width: 100%;
      // display: flex;
      // flex-direction: column;
      // justify-content: space-between;
      .price {
        color: red;
        font-weight: bold;
      }
      .info-numbox{
        float: right;
      }
    }
  }

  .cartfooter {
    position: fixed;
    width: 100%;
    height: 110px;
    font-size: 12px;
    // background-color:#f7f3f5;
    bottom: 0;
    display: block;
    border-top: 1px solid #fcdada;
    .left{
      font-size: 16px;  
      p{
        padding-left:12px;
        color: #ED662E;
        font-weight: 600px;
      }  
    }
    .right{
        float: right;
        height: 25px;
        top:-45px;
        margin-right: 20px;
      }
  }


  .he-similar{
    height: 60px;
    color: red; 
    font-weight: 600;
    text-align: center;   
  }

}
</style>
