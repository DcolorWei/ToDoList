<template>
  <div class="card-panel">
    <div class="icon" v-if="props.process.status == 2">
      <img src="@/assets/finish.gif" />
      <div>已完成</div>
    </div>
    <div class="icon" v-else-if="props.process.status == 1" @click="update()">
      <img src="@/assets/processing.gif" />
      <div>推进中</div>
    </div>
    <div class="icon" v-else @click="update()">
      <img src="@/assets/waiting.gif" />
      <div>待进行</div>
    </div>
    <div class="content">
      <div class="title">{{ props.process.title }}</div>
      <div class="describe">
        {{ props.process.describe }}
      </div>
      <div class="handle">{{ props.process.createTime }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, defineProps } from "vue";
const props = defineProps(["process"]);
const emits = defineEmits(["updatetask"]);

const update = () => {
  if (confirm(`修改进度为：${props.process.status ? "已完成" : "推进中"}？`)) {
    emits("updatetask", props.process.id);
  }
};
</script>

<style>
.card-panel {
  width: 80%;
  min-height: 20vh;
  margin: 2% 10%;
  border: 1px solid #fff;
  background-color: #fff;
  box-shadow: 1px 3px 4px 1px rgba(0, 0, 0, 0.2);
  border-radius: 6px;

  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.card-panel .icon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 20%;

  font-size: 0.85em;
  color: #7d7d7d;
}

.card-panel .icon img {
  width: 35px;
}

.card-panel .content {
  min-height: 10vh;
  width: 80%;
  text-align: left;
  padding: 5% 3% 1.5% 3%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

.card-panel .content .title {
  font-size: 18px;
  font-weight: 600;
  line-height: 30px;
}

.card-panel .content .describe {
  font-size: 16px;
  font-weight: 300;
  line-height: 18px;
}

.card-panel .content .handle {
  display: flex;
  justify-content: flex-end;
  line-height: 40px;
  bottom: 1px;
  font-size: 0.9em;
  height: 40px;
}
</style>
