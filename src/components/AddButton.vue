<template>
  <div>
  <el-button class="add-button" type="primary" @click="click">
    <el-icon><CirclePlus /></el-icon>
    <p class="el-font">ADD</p>
  </el-button>
  </div>
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
}
.el-font {
  font-family: script;
  font-size: 14px;
  font-weight: bold;
}

</style>
