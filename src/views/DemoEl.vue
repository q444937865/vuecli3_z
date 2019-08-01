<template>
  <div class="demoEl">
    <table-el-check :column="column" :dataSourse="dataSourse" :height="250"/>
  </div>
</template>

<script>
import TableElCheck from "@/components/TableElCheck.vue";
export default {
  name: "demoEl",
  components: {
    TableElCheck
  },
  data() {
    return {
      column: [],
      dataSourse: []
    };
  },
  created() {
    let arr = [];
    for (let i = 0; i < 30; i++) {
      arr.push({ name: "", lable: (i + 1).toString(), width: 80, prop: `check${i}`});
    }
    let data = [{ name: "风速风向传感器" }];
    for (let i = 0; i < 30; i++) {
      data[0][`check${i}`] = i % 2 == 0 ? true : false;
    }
    this.column = arr;
    this.dataSourse = data;
  }
};
</script>

<style lang="less" scoped>
.demoEl {
  width: 100%;
  height: 100%;
}
</style>