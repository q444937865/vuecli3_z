<template>
  <div class="table-el-check">
    <el-table :data="dataSourse" style="width: 100%" :height="height">
      <el-table-column fixed prop="name" label="" width="180"></el-table-column>
      <el-table-column
        v-for="(item,i) in column"
        :key="i"
        :prop="item.prop"
        :label="item.lable"
        :width="item.width"
      >
        <template slot-scope="scope">
          <span :class="'t-dot '+(scope.row[`check${i}`]?'bc-green':'bc-red')" @click="showdata(scope)"></span>
        </template>
      </el-table-column>
      <el-table-column fixed="right" prop="process" label width="180">
        <Zprocess :percent="50"/>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import Zprocess from "./Process-z";
export default {
  name: "table-el-check",
  components: {
    Zprocess
  },
  props: {
    column: {
      type: Array
    },
    dataSourse: {
      type: Array
    },
    height:{
      type: Number
    }
  },
  methods: {
    showdata(scope){
      console.log(scope);
    }
  },
};
</script>

<style scoped>
.table-el-check {
  width: 100%;
  height: 100%;
}
.table-el-check div {
  box-sizing: border-box;
}
.t-dot {
  display: inline-block;
  width: 8px;
  height: 8px;
  border-radius: 5px;
}
.bc-green {
  background-color: #67c23a;
}
.bc-red {
  background-color: red;
}
</style>