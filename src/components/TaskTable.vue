<template>
  <el-table :data="tableData" height="1000" style="width: 100%">
    <el-table-column prop="title" label="Title" width="200" />
    <el-table-column prop="description" label="Description" width="400" />
    <el-table-column prop="deadline" label="Deadline" width="200"/>
    <el-table-column prop="priority" label="Priority" width="200" />
    <el-table-column prop="completed" label="Is Complete" width="200">
      <template #default="scope">
        <el-checkbox v-model="scope.row.completed" />
      </template>
    </el-table-column>
    <el-table-column prop="action"  label="Action">
      <template #default="scope">
  <div>
    <div>
      <el-button
        class="update-button"
        type="primary"
        @click="updateRow(scope.row)"
        v-show="!scope.row.completed"
      >
        <el-icon><Edit /></el-icon>Update</el-button>
    </div>
    <div>
      <el-button
        class="delete-button"
        type="danger"
        @click="deleteRow(scope.row)"
      >
        <el-icon><Remove /></el-icon>Delete</el-button>
    </div>
  </div>
</template>

    </el-table-column>
  </el-table>
</template>
<script>
export default {
  name: 'TaskTable',
  components: {},
  props: {
    tableData: Array,
  },
  data() {
    return {
      
    };
  },
  methods: {
    updateRow(row) {
      this.$emit('edit', row);
    },
    deleteRow(row) {
      this.$message({
        message: 'The task is deleted successfully',
        type: 'success',
      });
      this.$emit('delete', row);
    },
  },
};

</script>
<style>
  .check-box{
    text-align: center;
  }
</style>

