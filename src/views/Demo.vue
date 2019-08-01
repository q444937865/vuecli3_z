<template>
  <div class="demo" style="width:800px;">
    <TableCheck :column="column" :dataSourse="dataSourse" :flWidth="flWidth"/>
  </div>
</template>

<script>
import TableCheck from "@/components/TableCheck.vue";

export default {
  name: "demo",
  components: {
    // HelloWorld,
    TableCheck
  },
  data() {
    return {
      column: [],
      dataSourse: [],
      flWidth: {
        firstWidth: 180,
        lastWidth: 180
      }
    };
  },
  created(){
    let arr = [];
    for (let i = 0; i < 30; i++) {
      arr.push({ name: i+1, width: 80 });
    }
    let data = [{ name: "风速风向传感器", data: [] }];
    for (let i = 0; i < 30; i++) {
      data[0].data.push({ check: i % 2 == 1 ? true : false });
    }
    this.column = arr;
    this.dataSourse = data;
  }
};
</script>

<style>
.demo{
  width: 100%;
}
</style>

