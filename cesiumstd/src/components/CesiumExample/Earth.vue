<template>
  <div class="home">
    <div id="cesiumContainer"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      map: {},
    };
  },
  components: {},
  created() {},
  mounted() {
    this.FirstCesium();
  },
  computed: {},
  methods: {
    initMap() {},
    FirstCesium() {
      new Cesium.Viewer("cesiumContainer",{
          animation:false,
          timeline:false
      });
      Cesium.Ion.defaultAccessToken =
        "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIzNzI3ZmZiYi03MWNmLTRiMzMtYTY2NS1iODU4MTU4NTk0NjYiLCJpZCI6MTEwNDQ5LCJpYXQiOjE2NjUyNzY1NTh9.GGDi2Q2GUYYfl0peA3_lhaNOE494NAUhN5UqktzFGhE";
    },
  },
};
</script>
<style scoped lang="scss">
.home {
  height: 100vh;
  #cesiumContainer {
    height: 100%;
    border: 1px solid gray;
  }
}
</style>