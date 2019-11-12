<template>
  <div>
<Classify-Header title="商品分类"></Classify-Header>
  <div class="calssify-con" >
        <div class="calssify-left" ref="wrapper">
            <ul class="calssify-left-ul" >
                <li v-for="item in goodslist" :key="item.id" @click="goDetail(item.id)" :class="{active:index===index}">
                    {{item.name}}
                </li>
            </ul>
        </div>
        <div class="calssify-rigth" ref="wrapper2">
            <ul class="calssify-left-ul">
                <li v-for="item in goodslist" :key="item.id" @click="goDetail(item.id)">
                     <img v-lazy="item.img_url">
                    <span>{{item.name}}</span>
                </li>
            </ul>
        </div>
    </div>
<v-footer></v-footer>
</div>
</template>


<script>
export default {
  data() {
    // data 是往自己组件内部，挂载一些私有数据的
    return {
      pageindex: 1, // 分页的页数
      goodslist: [] // 存放商品列表的数组
    };
  },
  created() {
    this.getGoodsList();
  },
  methods: {
    getGoodsList() {
      // 获取商品列表
      this.$http
        .get("api/getgoods?pageindex=" + this.pageindex)
        .then(result => {
          if (result.body.status === 0) {
            this.goodslist = this.goodslist.concat(result.body.message);
          }
        });
    },
    getMore() {
      this.pageindex++;
      this.getGoodsList();
    },
    goDetail(id) {
      // 使用JS的形式进行路由导航

      // 注意： 一定要区分 this.$route 和 this.$router 这两个对象，
      // 其中： this.$route 是路由【参数对象】，所有路由中的参数， params, query 都属于它
      // 其中： this.$router 是一个路由【导航对象】，用它 可以方便的 使用 JS 代码，实现路由的 前进、后退、 跳转到新的 URL 地址

      console.log(this);
      // 1. 最简单的
      // this.$router.push("/home/goodsinfo/" + id);
      // 2. 传递对象
      // this.$router.push({ path: "/home/goodsinfo/" + id });
      // 3. 传递命名的路由
      this.$router.push({ name: "goodsinfo", params: { id } });
    }
  }
};
</script>


<style lang="scss" scoped>
.active {
    border-left: 2px solid;
    background: #ffffff;
    color: #199cfe;
}

.calssify-con {
    display: flex;
    overflow: hidden;
    position: absolute;
    width: 100%;
    top: 0;
    bottom: 0;
    padding-top: 1.45rem;

    .calssify-left {
        flex: 0 0 2.9rem;
        width: 4rem;
        height: 100%;
        background: #f6f6f6;
        // border-right: 10px solid #f6f6f6;
        margin-bottom: 1.51rem;
        font-size: 0.35rem;

        li {
            height: 1.3rem;
            line-height: 1.3rem;
            text-align: center;
        }
    }

    .calssify-rigth {
        flex: 1;
        height: 100%;
        background: white;
        margin-bottom: 1.51rem;

        ul {
            display: flex;
            flex-wrap: wrap;

            li {
                display: flex;
                flex-direction: column;
                text-align: center;
                width: 33%;
                margin-top: 0.3rem;
                font-size: 0.34rem;
                float: left;

                img {
                    width: 1.98rem;
                    display: block;
                    margin: auto;
                }

                span {
                    color: #999;
                    line-height: 0.9rem;
                    font-size: 0.34rem;
                }
            }
        }
    }
}
</style>
