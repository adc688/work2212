<template>
  <div class="banner">
    <div class="title">
      <el-icon><List /></el-icon>
      FRAMEWORK
      <AddButton class="button" @click="add"></AddButton>
    </div>
  </div>
</template>

<script>
import AddButton from './AddButton.vue';
export default {
  name: 'Banner',
  components: {
    AddButton,
  },
  setup(props, { emit }) {
    function add() {
      emit('add');
    }
    return {
      add,
    };
  },
};
</script>

<style>
.banner {
  background-color: #1974D2;
  height: 70px;
  line-height: 70px;
  text-align: center;
}
.title {
  color: white;
  font-family: script;
  font-size: 18px;
  font-weight: bold;
}
.button {
  float: right;
  height: 70px;
  width: 25%;
}
.el-font {
  font-family: script;
  font-size: 14px;
  font-weight: bold;
}
</style>
