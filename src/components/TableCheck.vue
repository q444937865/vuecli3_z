<template>
  <div class="TableCheck" ref="TableCheck">
    <div class="normalTable">
      <table cellspacing="0" cellpadding="0" border="0" v-if="column.length" :width="sumWidth">
        <colgroup>
          <col ref="firstCol" :width="flWidth.firstWidth">
          <col v-for="(item,i) in column" :key="i" :width="item.width">
          <col ref="lastCol" :width="flWidth.lastWidth">
        </colgroup>
        <thead>
          <tr>
            <th></th>
            <th v-for="(item,i) in column" :key="i">{{item.name}}</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dtem,d) in dataSourse" :key="d">
            <th>{{dtem.name}}</th>
            <td v-for="(item,i) in dtem.data" :key="i">
              <span :class="'t-dot '+(item.check?'bc-green':'bc-red')"></span>
            </td>
            <td>
              <zProcess :percent="50" :height="10"></zProcess>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="fixedTable">
      <table cellspacing="0" cellpadding="0" border="0" v-if="column.length" :width="sumWidth">
        <colgroup>
          <col ref="firstCol" :width="flWidth.firstWidth">
          <col v-for="(item,i) in column" :key="i" :width="item.width">
          <col ref="lastCol" :width="flWidth.lastWidth">
        </colgroup>
        <thead>
          <tr>
            <th></th>
            <th class="hidden" v-for="(item,i) in column" :key="i">{{item.name}}</th>
            <th class="hidden"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dtem,d) in dataSourse" :key="d">
            <th>{{dtem.name}}</th>
            <td class="hidden" v-for="(item,i) in dtem.data" :key="i">
              <span :class="'t-dot '+(item.check?'bc-green':'bc-red')"></span>
            </td>
            <td class="hidden">
              <zProcess :percent="50" :height="10"></zProcess>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="fixedTableRight">
      <table cellspacing="0" cellpadding="0" border="0" v-if="column.length" :width="sumWidth">
        <colgroup>
          <col ref="firstCol" :width="flWidth.firstWidth">
          <col v-for="(item,i) in column" :key="i" :width="item.width">
          <col ref="lastCol" :width="flWidth.lastWidth">
        </colgroup>
        <thead>
          <tr>
            <th class="hidden"></th>
            <th class="hidden" v-for="(item,i) in column" :key="i">{{item.name}}</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(dtem,d) in dataSourse" :key="d">
            <th class="hidden">{{dtem.name}}</th>
            <td class="hidden" v-for="(item,i) in dtem.data" :key="i">
              <span :class="'t-dot '+(item.check?'bc-green':'bc-red')"></span>
            </td>
            <th>
              <zProcess :percent="50" :height="10"></zProcess>
            </th>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import zProcess from "./Process-z";

export default {
  name: "TableCheck",
  components: {
    zProcess
  },
  props: {
    column: {
      type: Array
    },
    dataSourse: {
      type: Array
    },
    flWidth: {
      default: () => {
        return { firstWidth: 180, lastWidth: 180 };
      },
      type: Object
    }
  },
  data() {
    return {
      sumWidth: 0
    };
  },
  mounted() {
    this.setWidth();
  },
  methods: {
    setWidth() {
      let sumWidth = 0;
      if (this.column.length) {
        this.column.map(item => {
          sumWidth += item.width;
        });
        let clientWidth = 0;
        if(this.$refs.TableCheck){
          clientWidth = this.$refs.TableCheck.clientWidth;
        }
        if (clientWidth > sumWidth) {
          sumWidth = clientWidth;
        }
        this.sumWidth = sumWidth;
      }
    }
  },
  watch: {
    column: {
      handler(val, oldVal) {
        console.log(val, oldVal);
        this.setWidth();
      },
      immediate: true
    },
    data: { 
      handler(val, oldVal) {
        console.log(val, oldVal);
      },
      immediate: true 
    }
  }
};
</script>

<style lang="less">
.TableCheck {
  overflow: hidden;
  width: 100%;
  position: relative;
  table {
    border: 1px;
    th,
    td {
      padding: 12px 2px;
      min-width: 0;
      box-sizing: border-box;
      text-overflow: ellipsis;
      vertical-align: middle;
      position: relative;
      text-align: center;
      border-bottom: 1px solid #ebeef5;
    }
    th {
      white-space: nowrap;
      overflow: hidden;
      user-select: none;
      background-color: #fff;
    }
  }
  .normalTable {
    width: 100%;
    overflow-x: auto;
  }
  .fixedTable {
    position: absolute;
    left: 0;
    top: 0;
  }
  .fixedTableRight {
    position: absolute;
    right: 0;
    left: auto;
    top: 0;
  }
  .hidden {
    visibility: hidden;
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
}
</style>