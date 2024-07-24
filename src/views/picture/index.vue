<template>
  <div class="map">
    <router-view></router-view>
    <div class="chooseMap">
      <el-radio-group v-model="radio">
        <el-radio label="1" class="myRadio">拓补图</el-radio>
        <el-radio label="2" class="myRadio">卫星图</el-radio>
      </el-radio-group>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      radio: this.$route.path === "/picture/index/topology" ? "1" : "2",
    };
  },
  watch: {
    radio(newVal) {
      if (newVal === "1") {
        this.$router.push("topology");
      } else if (newVal === "2") {
        this.$router.push("satellite");
      }
    },
  },
};
</script>

<style scoped>
.map {
  position: relative;
  height: 950px;
}

.chooseMap {
  z-index: 1;
  position: fixed;
  bottom: 50px;
  right: 80px;
}

.myRadio {
  /* background-color: #fff; */
  color: black;
  text-shadow: 2px 2px 4px #fff;
  font-weight: bold;
}
</style>