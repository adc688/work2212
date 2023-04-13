<template>
  <div>
    <Banner @add="add"></Banner>
    <TaskTable
      :tableData="tableData"
      @edit="edit"
      @delete="deleteItem"
    ></TaskTable>
    <AddTask
      ref="dialogRef"
      :tableData="tableData"
      :editInfo="editInfo"
      @handleSubmit="handleSubmit"
      @add="added"
    ></AddTask>
  </div>
</template>

<script>
import { ref } from 'vue';
import Banner from './components/Banner.vue';
import AddTask from './components/AddTask.vue';
import TaskTable from './components/TaskTable.vue';

export default {
  name: 'App',
  components: {
    Banner,
    TaskTable,
    AddTask,
  },
  setup() {
    let editInfo = ref(null);
    let dialogRef = ref(null);
    const tableData = ref([
      {
        title: 'justATest',
        description: 'description1',
        deadline: '04/12/2023',
        priority: 'High',
        completed: false,
      },
     {
        title: 'test2',
        description: 'description2',
        deadline: '04/12/2023',
        priority: 'Low',
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
