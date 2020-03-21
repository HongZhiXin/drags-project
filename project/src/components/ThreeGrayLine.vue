<template>
  <div class="container">
    <div class="item" />
    <div class="item" />
    <div class="item" />
  </div>
  
</template>
<script>
export default {
  name: "threeLine"
};
</script>
<style lang="less" scoped>
.container {
  width: 16px;
  height: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  .item {
    background-color:gray;
    opacity: 0.3;
    width: 100%;
    height: 1px;
  }
}
</style>