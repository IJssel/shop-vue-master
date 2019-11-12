# vue移动商城

## 项目结构

```
vue-cms
├─ .babelrc
├─ .gitignore
├─ dist
│  ├─ bundle.js
│  └─ index.html
├─ LICENSE
├─ node_modules
├─ package-lock.json
├─ package.json
├─ README.md
├─ src
│  ├─ App.vue
│  ├─ components
│  │  ├─ goods
│  │  │  ├─ GoodsComment.vue
│  │  │  ├─ GoodsDesc.vue
│  │  │  ├─ GoodsInfo.vue
│  │  │  └─ GoodsList.vue
│  │  ├─ news
│  │  │  ├─ NewsInfo.vue
│  │  │  └─ NewsList.vue
│  │  ├─ photos
│  │  │  ├─ PhotoInfo.vue
│  │  │  └─ PhotoList.vue
│  │  ├─ subcomponents
│  │  │  ├─ comment.vue
│  │  │  ├─ goodsinfo_numbox.vue
│  │  │  ├─ shopcar_numbox.vue
│  │  │  └─ swiper.vue
│  │  └─ tabbar
│  │     ├─ HomeContainer.vue
│  │     ├─ MemberContainer.vue
│  │     ├─ SearchContainer.vue
│  │     └─ ShopcarContainer.vue
│  ├─ images
│  
│  ├─ index.html
│  ├─ main.js
│  └─ router.js
└─ webpack.config.js

```



### 项目概要

- 本项目用到的技术栈： vue-cli + vue-router + vuex + axios + vue-axios +vue-preview+ mui(UI)+mintui(UI)
- 如何在本地运行本项目

```js
npm i 或 cnpm i      //安装项目依赖 建议使用淘宝镜像源 cnpm 安装 具体参考官网cnpm.taobao.org
npm run dev   //运行项目服务  在浏览器：localhost:8080/   查看
```

- 如果运行不成功请查看是否缺少配置文件 比如.babelrc或者尝试用vue-cli初始化一个vue项目再将本项目移植进去



## 项目展示

#### 首页

![2](\src\images\2.jpg)



#### 购物车

![3](.\src\images\3.png)

#### 图片展示

![4](.\src\images\4.png)

#### 个人中心

![5](.\src\images\5.png)
