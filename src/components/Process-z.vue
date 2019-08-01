<template>
  <div class="process">
    <div class="liner" ref="liner" :style="`height=${height}%`">
      <div class="liner-percent" ref="linerPercent" :style="`width=${percent}%`"></div>
    </div>
    <div class="percent">{{percent}}%</div>
  </div>
</template>

<script>
export default {
  name: "zProcess",
  props: {
    percent: {
      default: 0,
      type: Number
    },
    height: {
      default: 10,
      type: Number
    }
  },
  mounted() {},
  methods: {},
  watch: {
    percent: {
      handler(val, oldVal) {
        console.log(val, oldVal);
      },
      immediate: true
    }
  }
};
</script>

<style scoped>
.process {
  width: 100%;
  height: 16px;
  min-width: 120px;
  display: flex;
  align-items: center;
}
.process .liner {
  width: calc(100% - 40px);
  height: 10px;
  display: inline-block;
  background-color: #ccc;
  border-radius: 100px;
  overflow: hidden;
}
.process .liner .liner-percent {
  height: 100%;
  background: -webkit-linear-gradient(
    left,
    #0ef4ff,
    blue
  ); /* Safari 5.1 - 6.0 */
  background: linear-gradient(to right, #0ebbff, rgb(63, 103, 235));
}
.process .percent {
  width: 40px;
  text-align: center;
  display: inline-block;
  font-size: 14px;
}
</style>