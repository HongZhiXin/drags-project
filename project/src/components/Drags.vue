<template>
  <div>
    <draggable
      element="div"
      v-model="list"
      class="dragsList"
      animation="500"
      :component-data="getComponentData()"
    >
      <div v-for="(item,index) in list" :key="index">
        <div class="dragsItem">
          <span :class="flag?'isgray':''">{{index+1}}</span>
          <span>{{item.name}}</span>
          <ThreeGrayLine class="threeLine" v-if="!flag" />
        </div>
        <div class="grayLine" />
      </div>
    </draggable>
  </div>
</template>

<script>
// 引入拖拽组件
import draggable from "vuedraggable";
import ThreeGrayLine from "./ThreeGrayLine";
export default {
  name: "demo",
  components: {
    draggable,
    ThreeGrayLine
  },
  data() {
    return {
      list: [
        { name: "选项A" },
        { name: "选项B" },
        { name: "选项C" },
        { name: "选项D" }
      ],
      flag: false,
      Currindex: null
    };
  },
  methods: {
    handleChange(e) {
      this.flag = true;
      console.log("changed", e);
    },
    handleChoose(e) {
      const index = e.oldIndex;
      // const target = e.target
      // let currDOM = target.children[index];
      // console.log("onChoose", index,e);
      this.Currindex = index;
    },
    handleEnd(e) {
      setTimeout(() => {
        this.flag = false;
        this.Currindex = null;
      });
      console.log("end", e);
    },
    inputChanged(value) {
      this.activeNames = value;
    },
    getComponentData() {
      return {
        on: {
          change: this.handleChange,
          choose: this.handleChoose,
          end: this.handleEnd
        }
      };
    }
  }
};
</script>
<style lang="less" scoped>
.dragsList {
  width: 100%;
  .isgray {
    background: gray !important;
  }
  .grayLine {
    width: 100%;
    height: 1px;
    background: #f1f1f1;
  }
  .dragsItem {
    position: relative;
    background-color: #ffffff;
    height: 100px;
    line-height: 100px;
    display: flex;
    align-items: center;
    padding-left: 10px;
    > span {
      &:first-child {
        border-radius: 50%;
        width: 16px;
        height: 16px;
        background: cornflowerblue;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #fff;
        font-family: monospace;
      }
      &:nth-child(2) {
        margin-left: 10px;
        font-family: "微软雅黑";
      }
    }
  }
  .threeLine {
    position: absolute;
    right: 14px;
  }
}
</style>