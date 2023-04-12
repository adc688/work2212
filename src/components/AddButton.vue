<template>
  <el-button class="add-button" type="primary" @click="click">
    <el-icon><CirclePlus /></el-icon>
    <p class="el-font">ADD</p>
  </el-button>
</template>

<script>
export default {
  name: 'AddButton',
  setup(props, { emit }) {
    function click() {
      emit('click');
    }
    return {
      click,
    };
  },
};
</script>

<style>
.add-button {
  color: white;
  font-size: 14px;
  padding: 8px;
  height: 40px;
  width: 80px;
  line-height: 24px;
  margin-top: 15px;
  margin-right: 15px;
}
.el-font {
  font-family: script;
  font-size: 14px;
  font-weight: bold;
}
</style>
