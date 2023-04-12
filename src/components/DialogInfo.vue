<template>
  <div>
    <el-dialog width="380px" @open="open" @closed="closed" v-model="show">
      <template #header="{ close, titleId, titleClass }">
        <div class="my-header">
          <h4 id="titleId" class="titleClass">
            <el-icon>
              <Edit v-if="editInfo" />
              <CirclePlus v-else />
            </el-icon>
            {{ editInfo ? 'Edit Task' : 'Add Task' }}
          </h4>
        </div>
      </template>
      <el-form :model="form" label-width="100" :rules="rules" ref="formRef">
        <el-form-item v-if="!editInfo" label="Title" prop="title">
          <el-input v-model="form.title" />
        </el-form-item>
        <el-form-item label="Description" prop="description">
          <el-input v-model="form.description" />
        </el-form-item>
        <el-form-item label="Deadline" prop="deadline">
          <el-date-picker
            v-model="form.deadline"
            type="date"
            style="width: 100%"
            format="MM/DD/YYYY"
            value-format="MM/DD/YYYY"
          />
        </el-form-item>
        <el-form-item label="Priority" prop="priority">
          <el-radio-group v-model="form.priority">
            <el-radio label="Low">Low</el-radio>
            <el-radio label="Med">Med</el-radio>
            <el-radio label="High">High</el-radio>
          </el-radio-group>
        </el-form-item>

      </el-form>
      <template #footer>
        <el-button type="primary" @click="certain">
          <el-icon>
            <Edit v-if="editInfo" />
            <CirclePlus v-else />
          </el-icon>
          {{ editInfo ? 'Edit' : 'Add' }}
        </el-button>
        <el-button type="danger" @click="cancel">
          <el-icon><CircleClose /></el-icon>
          Cancel
        </el-button>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import { toRefs, ref, reactive } from 'vue';
import { h } from 'vue';
import { ElMessage } from 'element-plus';
export default {
  name: 'DialogInfo',
  props: { editInfo: Object, tableData: Array },
  setup(props, { emit }) {
    const rules = reactive({
      title: [
        {
          required: true,
          message: 'Please input title',
          trigger: 'blur',
        },
        {
          validator: (rule, value, callback) => {
            const repeat = props.tableData.some((i) => {
              if (i === props.editInfo) return false;
              if (i.title === value) return true;
              return false;
            });
            if (repeat) {
              callback(new Error('Title has exist!'));
            } else {
              callback();
            }
          },
          trigger: 'blur',
        },
      ],
      description: [
        {
          required: true,
          message: 'Discription is required!',
          trigger: 'blur',
        },
      ],
      deadline: [
        {
          required: true,
          message: 'Please select deadline!',
          trigger: 'blur',
        },
      ],
      priority: [
        {
          required: true,
          message: 'Please select priority!',
          trigger: 'blur',
        },
      ],
    });
    let form = ref(createForm());
    const formRef = ref(null);
    let show = ref(false);
    function certain() {
      formRef.value.validate().then(() => {
        if (props.editInfo) {
          ElMessage.success('The task was edited successfully');
          Object.assign(props.editInfo, form.value);
        } else {
          ElMessage.success('The task was added successfully');
          emit('add', form.value);
        }
        show.value = false;
      });
    }
    function createForm() {
      return {
        title: '',
        description: '',
        deadline: '',
        priority: '',
      };
    }
    function cancel() {
      show.value = false;
    }
    function open() {
      if (props.editInfo) {
        form.value = { ...props.editInfo };
      }
    }
    function closed() {
      form.value = createForm();
      formRef.value.clearValidate();
    }
    return {
      form,
      certain,
      cancel,
      show,
      formRef,
      open,
      closed,
      rules,
    };
  },
};
</script>
<style>
.my-header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  background-color: #1669f8;
  color: white;
}
</style>
