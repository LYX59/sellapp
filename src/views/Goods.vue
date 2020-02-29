<template>
  <div>
    <Row>
      <i-col span="6">
        <div class="godbox">
          <ul class="content">
            <div class="godfl">
              <div class="goodsfl" v-for="item in data" :key="item.name">{{item.name}}</div>
            </div>
          </ul>
        </div>
      </i-col>
      <i-col span="18">
        <div class="godpos">
          <div class="godfr">
            <div v-for="item in data" :key="item.id">
              <h5>{{ item.name }}</h5>
              <div class="box" v-for="child in item.foods" :key="child.id">
                <img :src="child.icon" />
                <div>
                  <h3>{{child.name}}</h3>
                  <p class="hui">{{child.description}}</p>
                  <span class="hui">月销售{{child.sellCount}}份</span>
                  <span class="hui">好评率{{child.rating}}%</span>
                  <p class="hong">
                    ￥{{child.price}}
                    <del>{{child.oldPrice}}</del>
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </i-col>
    </Row>
  </div>
</template>

<script>
import BScroll from "better-scroll";
import { getgoods } from "../api/apis";
export default {
  data() {
    return {
      data: {
        data: []
      }
    };
  },
  created() {
    getgoods().then(d => {
      this.data = d.data.data;
      console.log(d.data.data);
    });
  },
  mounted() {
    new BScroll(document.querySelector(".godbox"));
  }
};
</script>

<style lang="less" scoped>
* {
  margin: 0;
  padding: 0;
}
.godbox {
  background-color: #ccc;
  height: 320px;
    .godfl {
      width: 100px;
      height: 100%;
      overflow: scroll;
      .goodsfl {
        height: 60px;
        margin: 10px;
        display: flex;
        align-items: center;
      }
    }
  
}
.godpos {
  height: 320px;
  .godfr {
    width: 100%;
    height: 100%;
    overflow: scroll;
    justify-content: flex-start;
    .box {
      display: flex;
      justify-content: flex-start;
      margin: 10px 0;
      img {
        width: 100px;
      }
    }
  }
}
.hui {
  color: #ccc;
  font-size: 10px;
}
.hong {
  color: red;
  font-size: 14px;
}
</style>