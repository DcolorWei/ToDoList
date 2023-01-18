<template>
  <div class="form">
    <label>任务名称</label>
    <input v-model="form.taskName" />
    <label>详细内容</label>
    <textarea v-model="form.taskContent" />
  </div>
  <div class="handler">
    <div @click="cancel">取消</div>
    <div @click="confirm">确定</div>
  </div>
</template>

<script setup lang="ts">
import { reactive,defineEmits } from "vue";

const emit = defineEmits(["subi"]);
const form = reactive({
  taskName: "",
  taskContent: "",
  taskStatus: 0,
});
const cancel = () => {};
const confirm = () => {
  console.log(form);
  emit("subi",form);
};
</script>

<style>
.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 0 12vw;
  height: 80%;
}

.form label {
  font-size: 17px;
  font-weight: 600;
  margin-top: 20px;
}
.form input,
.form textarea {
  margin: 5px 0;
  font-size: 17px;
  width: 100%;
  border: 2px solid #6d6d6d;
  border-radius: 5px;
  padding-left: 6px;
}
.form input {
  height: 30px;
}

.form textarea {
  height: 80px;
  padding-top: 3px;
}
</style>
