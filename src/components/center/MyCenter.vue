<template>
  <div>
    <NavBack name="个人中心" @backjump="backjump"/>
    <!-- 头部 -->
    <div class="contentBox">
      <img class="myImg" :src="personMsg.logo" alt>
      <div class="userName">{{personMsg.name}}</div>
      <!-- <div class="userName navl">至尊</div> -->
      <div class="userName nums">{{personMsg.tel}}</div>
      <!-- <div class="msgBox">
        <mu-badge content="12" circle color="secondary">
          <mu-button icon>
            <mu-icon value="notifications" color="red"></mu-icon>
          </mu-button>
        </mu-badge>
      </div>-->
      <div class="setting">
        <img class="settingImg" src="../../assets/center/tiaoshi.png" alt>
      </div>
    </div>
    <!-- 主体内容 -->
    <!-- 资产 -->
    <div class="workingBox">
      <mu-row>
        <mu-col span="3" v-for="(items, ind) in dataLists" :key="ind">
          <div class="grid-cell" @click="jumpServer(ind)">
            <div class="imgServe numss">{{items.num}}</div>
            <div class="titleName name1">{{items.msg}}</div>
          </div>
        </mu-col>
      </mu-row>
    </div>
    <!-- 分列式主体内容 -->
    <div class="contentItemBox">
      <div class="contentItemsShow" @click="jumpMyResume">
        <img class="contentItemsImgs" src="../../assets/center/jianli.png" alt>
        <div class="myMsg">
          <span>我的简历</span>
          <div class="garid2"></div>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
      <div class="contentItemsShow" @click="jumpMyService">
        <img class="contentItemsImgs" src="../../assets/center/fuwu-copy.png" alt>
        <div class="myMsg">
          <span>我的服务</span>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
    </div>
    <div class="contentItemBox">
      <div class="contentItemsShow">
        <img class="contentItemsImgs" src="../../assets/center/rizhi.png" alt>
        <div class="myMsg">
          <span>个人日记</span>
          <div class="garid2"></div>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
      <div class="contentItemsShow" @click="jumpDataWork">
        <img class="contentItemsImgs" src="../../assets/center/richeng.png" alt>
        <div class="myMsg">
          <span>工作日程</span>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
    </div>
    <div class="contentItemBox">
      <div class="contentItemsShow">
        <img class="contentItemsImgs" src="../../assets/center/lianxikefu.png" alt>
        <div class="myMsg">
          <span>联系客服</span>
          <div class="garid2"></div>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
      <div class="contentItemsShow">
        <img class="contentItemsImgs" src="../../assets/center/tousujubao.png" alt>
        <div class="myMsg">
          <span>投诉举报</span>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
    </div>
    <div class="contentItemBox ssss">
      <div class="contentItemsShow lastShows">
        <img class="contentItemsImgs" src="../../assets/center/icon-test1.png" alt>
        <div class="myMsg">
          <span>更多</span>
        </div>
        <img class="forwardLogo" src="../../assets/forward@2x.png" alt>
      </div>
    </div>
    <div class="gesss"></div>
  </div>
</template>

<script>
import NavBack from "../public/NavBack1";
import logos from "../../assets/logoImg.jpg";

export default {
  name: "MyCenter",
  data() {
    return {
      personMsg: {
        logo: logos,
        name: "洛天依",
        tel: "135*****0385"
      },

      dataLists: [
        { num: "5222.34", msg: "余额" },
        { num: "1222.22", msg: "历史奖金" },
        { num: "6222.78", msg: "综合收入" },
        { num: "122.03", msg: "平台奖励" }
      ]
    };
  },
  components: { NavBack },
  methods: {
    backjump() {
      this.$router.push({
        path: "/"
      });
    },
    // 我的简历
    jumpMyResume() {
      this.$router.push({
        path: "/ResumeShow"
      });
    },
    // 我的服务
    jumpMyService() {
      this.$router.push({
        path: "/Service"
      });
    },

    // 工作日程
    jumpDataWork() {
      this.$router.push({
        path: "/DataWork"
      });
    },
    jumpServer(ind) {
      console.log(ind);
    }
  }
};
</script>

<style scoped>
.contentBox {
  background: repeating-linear-gradient(
      to top left,
      beige 0,
      beige 2em,
      moccasin 2em,
      moccasin 4em,
      wheat 4em,
      wheat 6em
    ),
    repeating-linear-gradient(
      to left,
      white 0,
      white 2em,
      wheat 2em,
      wheat 4em,
      beige 4em,
      beige 6em
    ),
    white;
  background-blend-mode: multiply;
  width: 100%;
  height: 2.4rem;
  margin: 0rem auto;
  /* background-color: white; */
  padding: 0.32rem;
  text-align: left;
  line-height: 2.4rem;
  position: relative;
}
.myImg {
  /* width: 2rem; */
  height: 1.76rem;
  border-radius: 50%;
}
.userName {
  font-size: 0.38rem;
  position: absolute;
  top: -0.28rem;
  left: 2.4rem;
  font-family: SimHei;
}
.nums {
  font-size: 0.28rem;
  top: 0.48rem;
}
.navl {
  left: 4.2rem;
  top: 0.68rem;
  font-size: 0.23rem;
  width: 1rem;
  height: 0.46rem;
  text-align: center;
  line-height: 0.46rem;
  border-radius: 0.46rem;
  background-color: #ee8018;
  color: white;
}
.setting {
  font-size: 0.38rem;
  position: absolute;
  top: -0.62rem;
  right: 0.32rem;
}
.settingImg {
  width: 0.48rem;
}
.workingBox {
  width: 100%;
  height: 1.6rem;
  padding-top: 0.1rem;
  background-color: #fff;
  margin: 0.32rem auto;
  position: relative;
}
.grid-cell {
  height: 1.82rem;
  color: #666666;
}
.imgServe {
  margin-top: 0.22rem;
  height: 0.6rem;
}
.titleName {
  font-size: 0.28rem;
  font-family: "Microsoft YaHei";
  color: #443d8b;
}
.garidBox {
  position: absolute;
  height: 1.36rem;
  border-left: solid 0.04rem #666666;
  top: 0.22rem;
  right: 1.78rem;
}
.numss {
  font-size: 0.32rem;
  color: #f6a623;
  margin: 0.12rem auto 0.06rem;
}
.name1 {
  color: #333333;
  font-family: SimHei;
}
.gesss {
  /* margin: 0.32rem auto; */
  width: 100%;
  height: 1.32rem;
  /* background-color: #333333; */
}
.gairds {
  width: 100%;
  border: 0.01rem solid #999999;
  position: absolute;
  top: 50%;
}
.contentItemBox {
  margin: 0.32rem auto;
  width: 100%;
  padding: 0.01rem 0.01rem 0.08rem 0.32rem;
  background-color: #fff;
}
.contentItemsShow {
  /* background-color: sandybrown; */
  text-align: left;
  position: relative;
  width: 100%;
  height: 0.84rem;
  line-height: 0.64rem;
  margin-top: 0.12rem;
  font-family: KaiTi;
}
.lastShows {
  height: 0.64rem;
}
.contentItemsImgs {
  width: 7%;
  margin-top: 0.08rem;
}
.myMsg {
  font-size: 0.32rem;
  position: absolute;
  left: 15%;
  display: inline-block;
  width: 85%;
  /* background-color: chartreuse; */
}
.forwardLogo {
  position: absolute;
  right: 0.32rem;
  width: 0.46em;
  top: 0.16rem;
}
.garid2 {
  width: 100%;
  border: solid 0.02rem #f9f9f9;
  margin-top: 0.2rem;
}
</style>