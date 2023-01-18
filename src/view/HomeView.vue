<template>
  <div class="banner">
    <img src="@/assets/list.gif" />
    <span>ToDoList</span>
  </div>
  <div>
    <div class="tools-bar">
      <Button color="#08C18A">新增任务</Button>
    </div>
    <List
      v-model:loading="loading"
      :finished="finished"
      finished-text="没有更多了"
      @load="onLoad"
    >
      <Card v-for="item in list" :key="item" :process="item" />
    </List>
  </div>

  <Popup>
    <TaskForm/>
  </Popup>
</template>

<script setup lang="ts">
import { ref, reactive, Ref } from "vue";
import { List, Button } from "vant";
import Card from "@/components/Card.vue";
import Popup from "@/components/Popup.vue";
import TaskForm from "@/components/TaskForm.vue";

const list: Ref<Array<any>> = ref([]);
const loading = ref(false);
const finished = ref(false);
const a=()=>{console.log("asas")}
const onLoad = () => {
  // 异步更新数据
  // setTimeout 仅做示例，真实场景中一般为 ajax 请求
  setTimeout(() => {
    list.value.push({
      status: Math.floor(Math.random() * 100) % 3,
      title: "标题bug" + Math.floor(Math.random() * 100),
      describe: Math.random() * 10000000,
    });
    // 加载状态结束
    loading.value = false;
    // 数据全部加载完成
    if (list.value.length >= 5) {
      finished.value = true;
    }
  }, 3000);
};
</script>

<style>
.banner {
  margin: 3vh 10vw 0 10vw;
  padding-bottom: 1vh;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  border-bottom: 0.5px solid silver;
}
.banner img {
  height: 60px;
}
.banner span {
  text-align: center;
  font-weight: 600;
  font-size: 30px;
  width: 50%;
}

.tools-bar {
  margin: 15px auto;
  display: flex;
  justify-content: space-around;
}

.tools-bar Button {
  font-size: 16px;
  font-weight: 600;
}
</style>
