
<template>
  <div class="box">
    <div ref="vantaRef" style="width: 100%; height: 1000px">
      <br>
      <h1> &nbsp; Welcome to TeamSphere！  </h1>
    </div>
  </div>

</template>

<script>
import * as THREE from "three";
import GLOBE from "vanta/src/vanta.globe";

export default {
  data() {
    return {};
  },
  mounted() {
    this.vantaEffect = GLOBE({
      el: this.$refs.vantaRef,
      THREE: THREE,
    });
    VANTA.GLOBE({
      el: this.$refs.vantaRef,
      /*以下为样式配置*/
      mouseControls: true,
      touchControls: true,
      gyroControls: false,
      minHeight: 200.00,
      minWidth: 200.00,
      scale: 1.00,
      scaleMobile: 1.00,
      color: 0x91aae3,
      backgroundColor: 0xf4f1f9,
    });
  },
  beforeDestroy() {
    if (this.vantaEffect) {
      this.vantaEffect.destroy();
    }
  },
};
</script>

<style lang="less" scoped>
.box {
  position: relative;
  .banner {
    z-index: 999;
    position: absolute;
    top: 30%;
    left: 10%;
    color: #fff;
  }
}
h1 {
  font-size: 66px;
}
p {
  margin-top: 60px;
  font-size: 18px;
}
</style>


