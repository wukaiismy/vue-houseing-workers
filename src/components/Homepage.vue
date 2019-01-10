<template>
  <div>
    <!-- 导航栏 -->
    <NavBack name="首页" @backjump="backjump"/>
    <!-- 主体内容 -->
    <!-- 个人荣誉信息展示 -->
    <!-- <div>
      <TimeShow/>
    </div>-->
    <div class="tianQiBox">
      <!--就这一句代码-->
      <iframe
        name="main"
        style="font-size:0.32rem"
        width="100%"
        scrolling="no"
        height="50"
        frameborder="0"
        allowtransparency="true"
        src="http://i.tianqi.com/index.php?c=code&id=12&icon=1&num=5"
      ></iframe>
    </div>
    <div class="personMsg">
      <span class="title">
        累计接单：
        <span class="showMsg">{{timeList.num}}</span> 次
      </span>
      <span class="title marJu">
        累计工作时长：
        <span class="showMsg">{{timeList.sum}}</span> 小时
      </span>
    </div>
    <!-- 消息跑马灯 -->
    <div class="msgShowBox">
      <!-- 配置slider组件 -->
      <slider ref="slider" :options="options" @slide="slide" @tap="onTap" @init="onInit">
        <slideritem v-for="(item,index) in pages" :key="index" :style="item.style">
          <div>
            <img class="logotz" :src="tongZhi" alt>
          </div>
          {{item.html}}
        </slideritem>
        <!-- 设置loading,可自定义 -->
        <div slot="loading">loading...</div>
      </slider>
    </div>
    <div class="navBoxShows">
      <circle-menu type="middle-around" asssa :number="4" animate="animated rubberBand" circle>
        <div slot="item_btn" class="itemBigBox">
          <img
            class="aMenuLogo"
            :class="seleted?'seleted':''"
            @click="changeMenu"
            :src="menuList.allMenu"
            alt
          >
          <div class="menuShou">菜单栏</div>
        </div>
        <div
          slot="item_1"
          :class="seleted1&&changeIndex=='1'?'seleted1':''"
          class="itemBoxs"
          @click="msgJump"
        >
          <img class="itemLogo" src="../assets/home/renwutixing.png" alt>
          <span class="itemTitle">消息</span>
        </div>
        <div
          slot="item_2"
          :class="seleted1&&changeIndex=='2'?'seleted1':''"
          class="itemBoxs"
          @click="otherJump"
        >
          <img class="itemLogo" src="../assets/home/qita1.png" alt>
          <span class="itemTitle">其他</span>
        </div>
        <div
          slot="item_3"
          :class="seleted1&&changeIndex=='3'?'seleted1':''"
          class="itemBoxs"
          @click="taskJump"
        >
          <img class="itemLogo" src="../assets/home/jiedanbaozhengjin.png" alt>
          <span class="itemTitle">接单</span>
        </div>
        <div
          slot="item_4"
          :class="seleted1&&changeIndex=='4'?'seleted1':''"
          class="itemBoxs"
          @click="workJump"
        >
          <img class="itemLogo" src="../assets/home/renwu.png" alt>
          <span class="itemTitle">任务</span>
        </div>
      </circle-menu>
    </div>
    <div class="footNbf"></div>
  </div>
</template>

<script>
import Foot from "./public/FootNavigation";
import Menus from "../assets/home/caidan.png";
import Menus1 from "../assets/home/caidan1.png";
import tongZhi from "../assets/home/tubiao-.png";
//在某个组件中
import CircleMenu from "vue-circle-menu";
import waves from "@/directive/waves"; // 水波纹指令
import NavBack from "./public/NavBack1";
import TimeShow from "./public/TimeShow";
import { slider, slideritem } from "vue-concise-slider"; // import slider component
import { mapGetters } from "vuex";

export default {
  name: "Homepage",
  directives: {
    waves
  },
  data() {
    return {
      tongZhi,
      timeList: {
        num: "20",
        sum: "150"
      },
      menuList: {
        allMenu: Menus
      },
      indexs: false,
      seleted: false,
      seleted1: false,
      changeIndex: "",
      list: ["第一条消息", "第二条消息", "第三条消息", "第四条消息"],
      //Image list
      pages: [],
      //Sliding configuration [obj]
      options: {
        pagination: false, // 底部小圆点是否隐藏（true显示，false隐藏）
        currentPage: 0, // 当前页码
        thresholdDistance: 500, // 滑动判定距离
        thresholdTime: 500, // 滑动判定时间
        autoplay: 3000, // 自动滚动[ms]
        loop: true, // 是否循环滚动
        direction: "vertical", // 滚动方向
        infinite: 1, // 无限滚动前后遍历数
        slidesToScroll: 1, // 滚动行数
        timingFunction: "ease",
        duration: 800,
        speed: 800
      }
    };
  },
  computed: {
    ...mapGetters(["roles", "name", "ids", "avatar", "power"])
  },
  created() {},
  mounted() {
    window.frames["main"].document.body.style.fontSize = 40 + "px";
    let that = this;
    setTimeout(function() {
      that.pages = [
        {
          html: "恭喜林忆莲喜提200元奖金",
          style: {
            background: "#fff",
            color: "#f6a623"
          }
        },
        {
          html: "恭喜张小花获得用户5.0评分",
          style: {
            background: "#fff",
            color: "#f6a623"
          }
        },
        {
          html: "恭喜苗翠花抢得双倍报酬订单",
          style: {
            background: "#fff",

            color: "#f6a623"
          }
        }
      ];
    }, 2000);
  },

  methods: {
    // Listener event
    slide(data) {
      // console.log(data)
    },
    onTap(data) {
      console.log(this.list[data.currentPage]);
    },
    onInit(data) {
      // console.log(data)
    },

    backjump() {
      this.$router.push({
        path: "/"
      });
    },
    // 点击消息按钮
    msgJump() {
      this.seleted1 = true;
      this.changeIndex = "1";
      setTimeout(() => {
        this.seleted1 = false;
        this.$router.push({
          path: "/MsgList"
        });
      }, 2000);
    },
    // 其他按钮
    otherJump() {
      console.log("您点击了其他按钮");
      this.seleted1 = true;
      this.changeIndex = "2";
      setTimeout(() => {
        this.seleted1 = false;
      }, 2000);
    },
    // 接单按钮
    taskJump() {
      console.log("您点击了接单按钮");
      this.seleted1 = true;
      this.changeIndex = "3";
      setTimeout(() => {
        this.seleted1 = false;
      }, 2000);
    },
    // 任务按钮
    workJump() {
      console.log("您点击了任务按钮");
      this.seleted1 = true;
      this.changeIndex = "4";
      setTimeout(() => {
        this.seleted1 = false;
        this.$router.push({
          path: "/Task"
        });
      }, 2000);
    },
    changeMenu() {
      this.indexs = !this.indexs;
      this.seleted = true;
      if (this.indexs == true) {
        this.menuList.allMenu = Menus1;
        setTimeout(() => {
          this.seleted = false;
        }, 1000);
      } else {
        this.menuList.allMenu = Menus;
        setTimeout(() => {
          this.seleted = false;
        }, 1000);
      }
    }
  },
  destroyed() {},
  components: { Foot, NavBack, CircleMenu, TimeShow, slider, slideritem }
};
</script>

<style scoped>
.personMsg {
  width: 100%;
  padding: 0.32rem;
  background-color: white;
  text-align: left;
  margin: 0.32rem auto;
}
.title {
  font-size: 0.3rem;
  color: #666666;
}
.marJu {
  display: inline-block;
  margin-left: 0.32rem;
}
.showMsg {
  color: #f6a623;
  font-size: 0.36rem;
}
.aMenuLogo {
  width: 100%;
}
.seleted {
  width: 100%;
  animation-name: myfirst;
  animation-duration: 1s;
  animation-timing-function: linear;
  animation-delay: 0s;
  animation-iteration-count: 2;
  animation-direction: alternate;
  animation-play-state: running;
  /* Firefox: */
  -moz-animation-name: myfirst;
  -moz-animation-duration: 1s;
  -moz-animation-timing-function: linear;
  -moz-animation-delay: 0s;
  -moz-animation-iteration-count: 2;
  -moz-animation-direction: alternate;
  -moz-animation-play-state: running;
  /* Safari and Chrome: */
  -webkit-animation-name: myfirst;
  -webkit-animation-duration: 1s;
  -webkit-animation-timing-function: linear;
  -webkit-animation-delay: 0s;
  -webkit-animation-iteration-count: 2;
  -webkit-animation-direction: alternate;
  -webkit-animation-play-state: running;
  /* Opera: */
  -o-animation-name: myfirst;
  -o-animation-duration: 1s;
  -o-animation-timing-function: linear;
  -o-animation-delay: 0s;
  -o-animation-iteration-count: 2;
  -o-animation-direction: alternate;
  -o-animation-play-state: running;
}

@keyframes myfirst {
  0% {
    width: 100%;
  }
  25% {
    width: 90%;
  }
  50% {
    width: 60%;
  }
  75% {
    width: 90%;
  }
  100% {
    width: 100%;
  }
}

@-moz-keyframes myfirst /* Firefox */ {
  0% {
    width: 100%;
  }
  25% {
    width: 90%;
  }
  50% {
    width: 60%;
  }
  75% {
    width: 90%;
  }
  100% {
    width: 100%;
  }
}

@-webkit-keyframes myfirst /* Safari and Chrome */ {
  0% {
    width: 100%;
  }
  25% {
    width: 90%;
  }
  50% {
    width: 60%;
  }
  75% {
    width: 90%;
  }
  100% {
    width: 100%;
  }
}

@-o-keyframes myfirst /* Opera */ {
  0% {
    width: 100%;
  }
  25% {
    width: 90%;
  }
  50% {
    width: 60%;
  }
  75% {
    width: 90%;
  }
  100% {
    width: 100%;
  }
}
.navBoxShows {
  width: 100%;
  height: 5rem;
  margin: 0.32rem auto;
  text-align: center;
  /* padding: 0.32rem; */
  background-color: #fff;
  position: relative;
}
.navBoxShows >>> .oy-menu-group {
  position: relative;
  top: 2rem;
  left: -41%;
  float: right;
  transition: 1s;
}
.navBoxShows >>> .oy-menu-btn {
  width: 1.2rem;
  height: 1.2rem;
  line-height: 1.3rem;
}
.navBoxShows >>> .pink {
  background: white;
}
.navBoxShows >>> .oy-menu-btn:active {
  box-shadow: none;
}
.itemBoxs {
  line-height: 0.2rem;
}
.itemLogo {
  width: 60%;
}
.itemTitle {
  font-size: 0.24rem;
  display: inline-block;
  margin-top: 0.08rem;
}
.navBoxShows
  >>> .middle-around
  .oy-menu-group.open
  .btn-list
  .oy-menu-item.oy-menu-item_1 {
  left: -1.8rem;
  top: 0;
}
.navBoxShows
  >>> .middle-around
  .oy-menu-group.open
  .btn-list
  .oy-menu-item.oy-menu-item_2 {
  left: 1.8rem;
  top: 0;
}
.navBoxShows
  >>> .middle-around
  .oy-menu-group.open
  .btn-list
  .oy-menu-item.oy-menu-item_3 {
  left: 1.1rem;
  top: -1.5rem;
}
.navBoxShows
  >>> .middle-around
  .oy-menu-group.open
  .btn-list
  .oy-menu-item.oy-menu-item_4 {
  left: -1.1rem;
  top: -1.5rem;
}
.navBoxShows >>> .oy-menu-item {
  width: 1.2rem;
  height: 1.2rem;
  line-height: 1.2rem;
  border-radius: 50%;
}
.navBoxShows >>> .yellow,
.navBoxShows >>> .purple,
.navBoxShows >>> .green,
.navBoxShows >>> .blue {
  background: #f9f9f9;
  border: #f6a623 solid 0.01rem;
  box-shadow: #666666 0px 1px 3px;
}
.menuShou {
  width: 100%;
  margin: 0.32rem auto;

  text-align: center;
  font-size: 0.34rem;
  color: #f6a623;
}
.itemBigBox {
  line-height: 0.2rem;
}
.seleted1 {
  -webkit-animation: rotateplane 1s 1 ease-in-out;
  animation: rotateplane 1s 1 ease-in-out;
}
@-webkit-keyframes rotateplane {
  0% {
    transform: perspective(120px) rotateY(0) rotateX(0);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(0);
  }
  50% {
    transform: perspective(120px) rotateY(0) rotateX(-180.1deg);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(-180.1deg);
  }
  75% {
    transform: perspective(120px) rotateY(-179.9deg) rotateX(-180deg);
    -webkit-transform: perspective(220px) rotateY(-179.9deg) rotateX(-180deg);
  }
  100% {
    transform: perspective(120px) rotateY(0) rotateX(0);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(0);
  }
}
@keyframes rotateplane {
  0% {
    transform: perspective(120px) rotateY(0) rotateX(0);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(0);
  }
  50% {
    transform: perspective(120px) rotateY(0) rotateX(-180.1deg);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(-180.1deg);
  }
  75% {
    transform: perspective(120px) rotateY(-179.9deg) rotateX(-180deg);
    -webkit-transform: perspective(220px) rotateY(-179.9deg) rotateX(-180deg);
  }
  100% {
    transform: perspective(120px) rotateY(0) rotateX(0);
    -webkit-transform: perspective(220px) rotateY(0) rotateX(0);
  }
}
.msgShowBox {
  width: 100%;
  padding: 0rem;
  height: 1rem;
  margin: 0.32rem auto;
  padding-left: 0.32rem;
  background-color: white;
}
.slider-item {
  font-size: 0.28rem;
}
.logotz {
  width: 0.46rem;
  position: absolute;
  top: 0.28rem;
  left: 0rem;
}
.tianQiBox {
  width: 100%;
  background-color: rgb(241, 218, 216);
  padding-left: 0.32rem;
}
.footNbf {
  width: 100%;
  height: 1.1rem;
  background-color: #f9f9f9;
}
.ssas {
  width: 0.88rem;
  height: 0.88rem;
}
.icon {
  width: 0.68rem;
  height: 0.68rem;
  vertical-align: 0.21rem;
  fill: #ee8018;
  overflow: hidden;
}
</style>