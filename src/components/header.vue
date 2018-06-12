<template>
  <div class="header">
      <div class="content-wrapper">
        <div class="avatar">
            <img width="64" height="64" :src="seller.src">
        </div> 
        <div class="content">
            <div class="title">
                <span class="brand"></span>
                <span class="name">{{seller.name}}</span>
            </div>
            <div class="description">
                {{seller.description}}/{{seller.deliveryTime}}
            </div>
            <div v-if="seller.supports"  class="support">
                <span class="icon" :class="classMap[seller.supports[0].type]"></span>
                <span class="text">{{seller.supports[0].description}}</span>
            </div>
        </div>
        <div v-if="seller.supports" class="support-count" @click="showDetail">
            <span class="count">{{seller.supports.length}}个</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>   
      </div>
      <div class="bulletin-wrapper" @click="showDetail">
           <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
      </div>
      <div class="background">
          <img :src="seller.src" width="100%" height="100%">
      </div>
      <transition name="fade" mode="out-in" >
        <div v-show="detailShow"  class="detail fade-transition">
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                    <h1 class="name">{{seller.name}}</h1>
                    <div class="star-wrapper">
                        <star :size='48' :score='4.5'></star>
                    </div>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">优惠信息</div>
                        <div class="line"></div>
                    </div>
                    <ul v-if="seller.supports" class="supports">
                        <li class="support-item" v-for="(item,index) in seller.supports">
                        <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                        <span class="text">{{seller.supports[index].description}}</span>
                        </li>
                    </ul>
                    <div class="title">
                        <div class="line"></div>
                        <div class="text">商家公告</div>
                        <div class="line"></div>
                    </div>
                    <div class="bulletin">
                        <p class="content">{{seller.bulletin}}</p>
                    </div>
                </div>
            </div>
            <div class="detail-close" @click="hideDetail">X</div>
        </div>
      </transition>
      
  </div>
</template>

<script>
import star from "./star";
export default {
  name: "header",
  props: ['seller'],
  data() {
    return {
      detailShow: false
    };
  },
  created() {
    this.classMap = ["decrease", "discount", "special", "invoice", "guarantee"];
  },
  methods: {
    showDetail() {
      this.detailShow = true;
    },
    hideDetail() {
      this.detailShow = false;
    }
  },
  components:{
      star
  }
};
</script>
<style scoped>
.bgc {
  background-color: red;
}
.header .detail .detail-wrapper .detail-main .name {
    line-height: 16px;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
}
.header .detail .detail-wrapper .detail-main .supports .support-item .text {
    line-height: 16px;
    font-size: 12px;
}
.header .detail .detail-close {
    position: relative;
    width: 32px;
    height: 32px;
    margin: -64px auto 0 auto;
    clear: both;
    font-size: 32px;
}
.header .detail {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  transition: all 0.5s;
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
}
.header .detail.fade-transition {
    opacity: 1;
    background: rgba(7,17,27,0.8);
}
.header .detail .detail-wrapper .detail-main .supports {
    width: 80%;
    margin: 0 auto;
}
.header .detail .detail-wrapper .detail-main .supports .support-item {
    padding: 0 12px;
    margin-bottom: 12px;
    font-size: 0;
}
/* .header .fade-enter-active {
    opacity: 0;
    background: rgba(7,17,27,0);
} */
/* .header .fade-leave-active {
    opacity: 0;
    background: rgba(7, 17, 27, 0);
} */
.header .detail.fade-enter {
    opacity: 0;
    background: rgba(7, 17, 27, 0);
}

.header .detail.fade-leave-to  {
    opacity: 0;
    background: rgba(7, 17, 27, 0);
}

.header .bulletin-wrapper .bulletin-text {
  vertical-alignrgba(90, 92, 94, 0)
  margin: 0 4px;
  font-size: 10px;
}
.header .content-wrapper .support-count .count {
  vertical-align: top;
  font-size: 10px;
}
.header .bulletin-wrapper {
  position: relative;
  height: 28px;
  line-height: 28px;
  padding: 0 22px 0 12px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  background: rgba(7, 17, 27, 0.2);
}
.header {
  position: relative;
  overflow: hidden;
  color: #ffffff;
  background: rgba(7, 17, 27, 0.5);
}
.header .content-wrapper .avatar img {
  border-radius: 2px;
}
.header .content-wrapper {
  position: relative;
  padding: 24px 12px 18px 24px;
  font-size: 0;
}
.header .content-wrapper .avatar {
  display: inline-block;
  vertical-align: top;
}
.header .content-wrapper .content {
  display: inline-block;
  margin-left: 16px;
}
.header .content-wrapper .content .title {
  margin: 2px 0 8px 0;
}
.header .content-wrapper .content .description {
  margin-bottom: 10px;
  line-height: 12px;
  font-size: 12px;
}
.header .content-wrapper .content .title .brand {
  display: inline-block;
  vertical-align: top;
  width: 30px;
  height: 18px;
  background-image: url(../assets/brand@2x.png);
  background-size: 30px 18px;
  background-repeat: no-repeat;
}
.header .content-wrapper .content .support .icon.decrease {
  background-image: url(../assets/decrease_1@2x.png);
}
.header .content-wrapper .content .title .name {
  margin-left: 6px;
  font-size: 16px;
  line-height: 18px;
  font-weight: bold;
}
.header .content-wrapper .content .support .icon {
  display: inline-block;
  vertical-align: top;
  width: 12px;
  height: 12px;
  margin-right: 4px;
  background-size: 12px 12px;
  background-repeat: no-repeat;
}
.header .content-wrapper .content .support .text {
  line-height: 12px;
  font-size: 10px;
}
.header .content-wrapper .support-count {
  position: absolute;
  right: 12px;
  bottom: 14px;
  padding: 0 8px;
  height: 24px;
  line-height: 24px;
  border-radius: 14px;
  background: rgba(0, 0, 0, 0.2);
  text-align: center;
}
.header .content-wrapper .support-count .icon-keyboard_arrow_right {
  margin-left: 2px;
  line-height: 24px;
  font-size: 10px;
}
[class^="icon-"],
[class*=" icon-"] {
  font-family: "sell-icon" !important;
  speak: none;
  font-style: normal;
  font-weight: normal;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.icon-keyboard_arrow_right:before {
  content: "\E909";
}
.header .background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  -webkit-filter: blur(10px);
  filter: blur(10px);
}
.header .detail .detail-wrapper {
    width: 100%;
    min-height: 100%;
}
.clearfix {
    display: inline-block;
}
.clearfix:after {
    display: block;
    content: ".";
    height: 0;
    line-height: 0;
    clear: both;
    visibility: hidden;
}
.header .detail .detail-wrapper .detail-main {
    margin-top: 64px;
    padding-bottom: 64px;
}
header .detail .detail-wrapper .detail-main .name {
    line-height: 16px;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
}
.header .detail .detail-wrapper .detail-main .star-wrapper {
    margin-top: 18px;
    padding: 2px 0;
    text-align: center;
}
.header .detail .detail-wrapper .detail-main .title {
    display: -ms-flexbox;
    display: flex;
    width: 80%;
    margin: 28px auto 24px auto;
}
.header .detail .detail-wrapper .detail-main .title .line {
    -ms-flex: 1;
    flex: 1;
    position: relative;
    top: -6px;
    border-bottom: 1px solid rgba(255,255,255,0.2);
}
.header .detail .detail-wrapper .detail-main .title .text {
    padding: 0 12px;
    font-weight: 700;
    font-size: 14px;
}

.header .detail .detail-wrapper .detail-main .title .line {
    -ms-flex: 1;
    flex: 1;
    position: relative;
    top: -6px;
    border-bottom: 1px solid rgba(255,255,255,0.2);
}
.header .detail .detail-wrapper .detail-main .bulletin {
    width: 80%;
    margin: 0 auto;
}
.header .detail .detail-wrapper .detail-main .bulletin .content {
    padding: 0 12px;
    line-height: 24px;
    font-size: 12px;
}
</style>
