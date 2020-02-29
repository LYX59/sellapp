<template>
  <div>
    <!-- 容器页面 -->
    <div class="top_box">
      <div class="bjimg" :style="{background:'url('+data.avatar+')'}"></div>
      <Row>
        <i-col span="8" class="imgbox">
          <img :src="data.avatar" />
        </i-col>
        <i-col span="12" class="topimg">
          <h3>
            <img src="../assets/imgs/brand@2x.png" alt />
            {{data.name}}
          </h3>
          <p>{{data.description}}/{{data.deliveryTime}}分钟送达</p>
          <p>
            <img src="../assets/imgs/decrease_1@2x.png" alt />
            {{data.supports[0].description}},满50减10
          </p>
        </i-col>
        <i-col span="4">
          <div class="btn">
            <i-button shape="circle" size="small">5个></i-button>
          </div>
        </i-col>
      </Row>
    </div>
    <div class="bulletin">
        <img src="../assets/imgs/bulletin@2x.png" alt="">
{{data.bulletin}}
    </div>
    <div class="router-link-div">
      <router-link class="rou" to="/goods">商品</router-link>
      <router-link class="rou" to="/evaluate">评价</router-link>
      <router-link class="rou" to="/merchant">商家</router-link>
    </div>

    <!-- 二级路由出口 -->
    <router-view></router-view>

    <div class="shopcar-bar">购物车条</div>
  </div>
</template>

<script>
import { getSeller } from "../api/apis";
export default {
  data() {
    return {
      data: { supports: [{ description: "" }] } //商家信息
    };
   
  },
  created() {
    //发送初始化请求
    //   var obj =  getSeller() // req.get('/api/seller')
    //     // obj === req.get('/api/seller')
    //     obj.then()

    getSeller().then(d => {
      // 怎么把商家数据渲染到屏幕上？？？
      this.data = d.data.data;
    });
  }
};
</script>

<style lang="less" scoped>
img {
  margin: 0;
  padding: 0;
}
.router-link-div {
  display: flex;
  justify-content: space-around;
  .rou{
     height: 60px; 
     font-size: 16px;
     display: flex;
     align-items: center;
  }
}

.shopcar-bar {
  position: fixed; //脱离文档流-相对于浏览器绝对定位
  height: 60px;
  width: 100%;
  bottom: 0; //永远挨着浏览器底边
  background-color: #141c27;
}
.top_box {
  height: 120px;
  .bjimg {
    width: 100%;
    height: 120px;
    position: absolute;
    top: 0;
    left: 0;
    background: cover;
    z-index: -1;
    filter: blur(5px);
    background-position: center;
  }
  .imgbox {
    img {
      width: 70px;
    }
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .topimg {
    margin-top: 20px;
    h3 {
      display: flex;
      align-items: center;
      img {
        width: 35px;
      }
    }
    p {
      display: flex;
      align-items: center;
      img {
        width: 20px;
      }
    }
  }
  .btn {
    height: 100px;
    position: absolute;
    text-align: center;
    top: 62px;
  }
}
.bulletin{
    width: 100%;
    height: 30px;
    overflow:hidden;
    text-overflow:ellipsis;
    white-space:nowrap;
        display: flex;
    align-items: center;
background:rgba(0,0,0,0.1);
color: #fff;
}
</style>
