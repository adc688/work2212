<template>
  <div>
    <Banner @add="add"></Banner>
    <TaskTable
      :tableData="tableData"
      @edit="edit"
      @delete="deleteItem"
    ></TaskTable>
    <DialogInfo
      ref="dialogRef"
      :tableData="tableData"
      :editInfo="editInfo"
      @handleSubmit="handleSubmit"
      @add="added"
    ></DialogInfo>
  </div>
</template>

<script>
import { ref } from 'vue';
import Banner from './components/Banner.vue';
import DialogInfo from './components/DialogInfo.vue';
import TaskTable from './components/TaskTable.vue';

export default {
  name: 'App',
  components: {
    Banner,
    TaskTable,
    DialogInfo,
  },
  setup() {
    let editInfo = ref(null);
    let dialogRef = ref(null);
    const tableData = ref([
      {
        title: 'try1',
        description: 'description1',
        deadline: '04/12/2023',
        priority: 'High',
        completed: false,
      },
    ]);
    let row = ref(null);

    function add() {
      editInfo.value = null;
      dialogRef.value.show = true;
    }
    function edit(row) {
      editInfo.value = row;
      dialogRef.value.show = true;
    }
    const handleSubmit = (val) => {
      console.log('receive data：', val);
    };

    function deleteItem(row) {
      tableData.value = tableData.value.filter((i) => i !== row);
    }
    function added(row) {
      tableData.value.push(row);
    }

    return {
      add,
      handleSubmit,
      dialogRef,
      editInfo,
      tableData,
      edit,
      deleteItem,
      added,
    };
  },
};
</script>

<style></style>
