<template>
  <div id="app">
    <my-header :seller='seller'></my-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <keep-alive>

    <router-view></router-view>
    </keep-alive>

  </div>
</template>

<script>
import header from "./components/header";

export default {
  name: "App",
  data() {
    return {
      seller: {
        id: (() => {
          let objs = {
            name: "haha"
          };
          return objs;
        })()
      }
    };
  },
  created() {
    console.log(this.seller.id.name);
    //模拟数据请求成功时返回的数据
    var res = {
      id: "我是id",
      age: "22",
      come: "beijing",
      src:
        "http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg",
      name: "粥品香坊（西二旗）",
      description: "蜂鸟专送",
      deliveryTime: 38,
        "bulletin": "粥品香坊其烹饪粥料的秘方源于中国千年古法，在融和现代制作工艺，由世界烹饪大师屈浩先生领衔研发。坚守纯天然、0添加的良心品质深得消费者青睐，发展至今成为粥类的引领品牌。是2008年奥运会和2013年园博会指定餐饮服务商。",
      supports: [
        {
          type: 0,
          description: "在线支付满28减5"
        },
        {
          type: 1,
          description: "VC无限橙果汁全场8折"
        },
        {
          type: 2,
          description: "单人精彩套餐"
        },
        {
          type: 3,
          description: "该商家支持发票,请下单写好发票抬头"
        },
        {
          type: 4,
          description: "已加入“外卖保”计划,食品安全保障"
        }
      ]
    };
    this.seller = Object.assign({}, this.seller, res);
  },
  components: {
    "my-header": header
  }
};
</script>

<style>

.tab {
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  border-bottom: 1px solid rgba(7, 17, 27, 0.1);
  border-bottom: 1px solid rgba(7, 17, 27, 0.1);
}
.tab-item {
  flex: 1;
  text-align: center;
}
.tab-item a {
  display: block;
  font-size: 14px;
  color: rgb(77, 85, 93);
}
.tab-item  .router-link-active {
  color: rgb(240, 20, 20);
}
.ads {
  background-color: red;
}
</style>
