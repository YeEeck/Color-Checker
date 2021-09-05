<template>
  <div class="warp">
    <div class="top-bar">
      <span>等级：{{ level }}</span
      ><br />
      <span>得分：{{ point }}</span>
    </div>
    <div
      class="home"
      :style="{ backgroundColor: colorOut }"
      @click="errorPoint"
    >
      <div
        class="test-div"
        :style="{
          backgroundColor: colorOutg,
          top: top + 'px',
          left: left + 'px',
        }"
        @click="divClicked"
      ></div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      red: 255,
      blue: 0,
      green: 0,
      redg: 245,
      blueg: 0,
      greeng: 0,
      top: 50,
      left: 0,
      level: 0,
      point: 0,
      lastTime: 0,
    };
  },
  mounted() {
    this.lastTime = Date.parse(new Date());
  },
  methods: {
    divClicked() {
      this.level += 1;
      let addonPoint = 5000 - (Date.parse(new Date()) - this.lastTime);
      this.lastTime = Date.parse(new Date());
      if (addonPoint <= 0) addonPoint = 1000;
      this.point += this.level * 10 * (addonPoint / 1000) + 1000;
      this.red = Math.floor(Math.random() * 255);
      this.blue = Math.floor(Math.random() * 255);
      this.green = Math.floor(Math.random() * 255);
      this.redg = this.red;
      this.blueg = this.blue;
      this.greeng = this.green;

      this.redg -= 10 - (this.level / 10);

      this.greeng -= 10 - (this.level / 10);

      this.blueg -= 10 - (this.level / 10);

      this.left = Math.floor(Math.random() * 450);
      this.top = Math.floor(Math.random() * 450);
    },

    errorPoint() {
      this.point -= 1000;
    },
  },
  computed: {
    colorOut() {
      return "rgb(" + this.red + "," + this.green + "," + this.blue + ")";
    },
    colorOutg() {
      return "rgb(" + this.redg + "," + this.greeng + "," + this.blueg + ")";
    },
  },
};
</script>

<style>
.test-div {
  /* background-color: royalblue; */
  width: 50px;
  height: 50px;
  position: relative;
}
.home {
  width: 500px;
  height: 500px;
}
.warp {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}
</style>