<template>
  <div>
    <NavBack name="我的服务" @backjump="backjump"/>
    <div>暂时不晓得写什么</div>
  </div>
</template>

<script>
import NavBack from "../../public/NavBack";
export default {
  name: "Service",
  components: { NavBack },
  data() {
    return {};
  },
  methods: {
    backjump() {
      this.$router.push({
        path: "/MyCenter"
      });
    }
  }
};
</script>

<style scoped>
</style>