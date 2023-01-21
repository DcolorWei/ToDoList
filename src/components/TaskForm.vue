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
import { reactive, defineEmits } from "vue";

const emits = defineEmits(["add"]);
const form = reactive({
  taskName: "",
  taskContent: "",
  taskStatus: 0,
});
const cancel = () => {
  emits("add");
};
const confirm = () => {
  console.log(form)
  emits("add", form);
};
</script>

<style>
.form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  padding: 0 12vw;
  height: 65%;
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
  height: 24px;
}

.form textarea {
  height: 80px;
  padding-top: 3px;
}

.handler {
  display: flex;
  flex-direction: row;
  margin: 20px auto;
  width: 60%;
  height: 35%;
  justify-content: space-between;
  align-items: center;
}
.handler div {
  width: 60px;
  height: 20px;
  padding: 6px;
  border-radius: 5px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}

.handler div:nth-child(1) {
  background-color: #9d9d9d;
  color: #fff;
}
.handler div:nth-child(2) {
  background-color: #07c189;
  color: #fff;
}
</style>
