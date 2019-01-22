<template>
  <div>
    <NavBack name="确认客户信息" @backjump="backjump"/>
    <div class="bigBoxShows">
      <div class="addMsg">
        <span class="addTitle">验证码</span>
        <div class="rightBox">
          <input
            type="number"
            v-model="dataMsgAddress.yzm"
            class="rightBoxIpt"
            placeholder="输入客户提供的验证码"
          >
        </div>
        <div class="gaird1"></div>
      </div>
      <!-- 地图显示位置 -->
      <div class="amap-wrapper">
        <el-amap class="amap-box" vid="map" :zoom="zoom" :center="center" :plugin="plugin">
          <el-amap-marker ref="menuItem" vid="marker" :position="center" :label="label"></el-amap-marker>
          <el-amap-circle
            vid="circle"
            :center="center"
            :radius="radius"
            fill-opacity="0.2"
            strokeColor="#38f"
            strokeOpacity="0.8"
            strokeWeight="1"
            fillColor="#38f"
          ></el-amap-circle>
        </el-amap>
        <div class="addes">{{address}}</div>
      </div>
      <div class="submitAdd" v-waves @click="submitJump">开始工作</div>
    </div>
  </div>
</template>

<script>
import NavBack from "../public/NavBack";
import waves from "@/directive/waves"; // 水波纹指令
export default {
  name: "MapDemo",

  components: { NavBack },
  directives: {
    waves
  },
  data() {
    let vm = this;
    return {
      switchVal: {
        value1: false
      },
      dataMsgAddress: {
        yzm: "",
        name: "",
        tel: ""
      },
      zoom: 16,
      center: [121.406051, 31.179695],
      label: {
        content: "您的位置",
        offset: [10, 12]
      },
      address: "",
      radius: 50,

      plugin: [
        // {
        //   pName: "OverView"
        //   //isOpen:true//鹰眼是否打开
        // },
        {
          pName: "Scale"
        },
        {
          pName: "Geolocation", //定位插件
          showMarker: false,
          events: {
            init(o) {
              //定位成功 自动将marker和circle移到定位点
              o.getCurrentPosition((status, result) => {
                console.log(result);
                vm.center = [result.position.lng, result.position.lat];
                vm.label.content = result.formattedAddress;
                console.log(vm.label);
              });
            }
          }
        }
      ]
    };
  },
  watch: {
    label: {
      handler(val) {
        this.getMsg(val);
      },
      immediate: true,
      deep: true
    }
  },

  methods: {
    backjump() {
      this.$router.push({
        path: "/SubmitOrders"
      });
    },
    getMsg(val) {
      this.address = this.label.content;
    },
    changeMsg() {
      console.log(this.switchVal.value1);
    },
    // 保存地址
    submitJump() {
      var data_list = {
        yzm: this.dataMsgAddress.yzm,
        lat: this.center[1],
        ing: this.center[0],
        address: this.label.content
      };
      console.log(data_list);
      this.$router.push({
        path: "/WorkingShow"
      });
    }
  }
};
</script>

<style scoped>
.HomeBox {
  background-color: #f9f9f9;
  width: 100%;
  /* position: fixed; */
  height: 100%;
}
.navBox {
  height: 1.28rem;
  width: 100%;
  background-image: linear-gradient(-137deg, #ee8018 0%, #fbda61 100%);
  position: fixed;
  z-index: 100000;
}
.Bas {
  width: 100%;
  height: 0.4rem;
}
.gaidm {
  width: 100%;
  height: 1.28rem;
}

.amap-wrapper {
  height: 300px;
}
.search-box {
  position: absolute;
  top: 25px;
  left: 20px;
  width: 5rem;
}
.bigBoxShows {
}
.addMsg {
  width: 100%;
  padding: 0.32rem 0.32rem 0 0.32rem;
  background-color: #fff;
  position: relative;
  text-align: left;
  /* line-height: 100%; */
  /* background-color: palegoldenrod; */
}
.addTitle {
  font-size: 0.3rem;
  position: absolute;
  /* letter-spacing: 0.06rem; */
}

.rightBox {
  width: 85%;
  padding-left: 0.32rem;
  /* background-color: #fbda61; */
  position: relative;
  margin-left: 1.2rem;
  top: 0rem;
  /* right: 0; */
}
.rightBoxLocalImg {
  width: 0.46rem;
}
.rightBoxLocalDetail {
  font-size: 0.28rem;
  color: #999999;
  position: relative;
  left: 0.32rem;
  top: -0.07rem;
}
.rightBoxLocalForward {
  width: 0.14rem;
  position: absolute;
  right: 0.21rem;
  top: 0.12rem;
}
.gaird1 {
  width: 100%;
  border: #f9f9f9 solid 0.02rem;
  margin-top: 0.32rem;
}
.rightBoxIpt {
  width: 90%;
  height: 100%;
  outline: none;
  border-width: 0;
  caret-color: #ee8018;
  font-size: 0.3rem;
}
.shuoMing {
  width: 80%;
  font-size: 0.24rem;
  margin-top: 0.64rem;
  /* background-color: aqua; */
}
.select-control-row {
  position: absolute;
  /* background-color: palegoldenrod; */
  top: 0.82rem;
  right: 0.32rem;
}
.mu-switch {
  height: 0.64rem;
  line-height: 0.64rem;
}
.select-control-row >>> .mu-switch-wrapper {
  width: 100%;
  height: 0.64rem;
}
.select-control-row >>> .mu-switch-container {
  width: 0.76rem;
  padding: 0.08rem 0 0.08rem 0.04rem;
  margin-right: 0.16rem;
}
.select-control-row >>> .mu-switch-track {
  width: 100%;
  height: 0.28rem;
  border-radius: 0.6rem;
}
.select-control-row >>> .mu-switch-thumb {
  position: absolute;
  top: 1px;
  left: 0;
  width: 0.4rem;
  height: 0.4rem;
  line-height: 0.48rem;
}
.select-control-row >>> .mu-switch-checked {
  color: #ee8018;
}
.select-control-row >>> .mu-switch-checked .mu-switch-thumb {
  transform: translate3d(0.36rem, 0, 0);
}
.select-control-row >>> .mu-switch-ripple-wrapper {
  top: -0.2rem;
  left: -0.2rem;
}
.submitAdd {
  width: 100%;
  height: 0.88rem;
  background-color: #ee8018;
  font-size: 0.36rem;
  color: #fff;
  line-height: 0.88rem;
  margin: 1rem auto;
}
.showLocal {
  width: 70%;
  font-size: 0.3rem;
}
/* 地图样式 */
.amap-wrapper {
  height: 5rem;
  margin: 0.32rem auto;
}
.addes {
  margin: 0.22rem auto;
  background-color: white;
  width: 100%;
  height: 0.88rem;
  line-height: 0.88rem;
  font-size: 0.3rem;
  color: #ee8018;
}
</style>