<template>
  <div class="banner">
    <img src="@/assets/list.gif" />
    <span>ToDoList</span>
  </div>
  <div>
    <div class="tools-bar">
      <Button color="#08C18A" @click="(e) => hide(e)">新增任务</Button>
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

  <Popup v-model:show="showPopup" style="border-radius: 5px">
    <TaskForm @add="(e) => hide(e)" />
  </Popup>
</template>

<script setup lang="ts">
import { ref, reactive, Ref } from "vue";
import axios from "axios";
import { List, Button, Popup } from "vant";
import Card from "@/components/Card.vue";
import TaskForm from "@/components/TaskForm.vue";

const list: Ref<Array<any>> = ref([]);
const loading = ref(false);
const finished = ref(false);

const showPopup = ref(false);

function hide(e: { taskName: string; taskContent: string; taskStatus: 0 }) {
  showPopup.value = !showPopup.value;
  if (e && e.taskName && e.taskContent) {
    axios({
      url: "http://122.9.107.17:39443/v3/task",
      method: "POST",
      data: e,
    }).then(() => {
      getData();
    });
  }
}

const onLoad = () => {
  getData();
};

const getData = () => {
  loading.value = true;
  finished.value = false;
  list.value = [];
  axios({
    url: "http://122.9.107.17:39443/v3/task",
  }).then((res) => {
    console.log(res.data);
    res.data.forEach(
      (i: {
        id: number;
        taskName: string;
        status: 0 | 1 | 2;
        taskContent1?: string;
        taskContent2?: string;
        taskContent3?: string;
        createTime: string;
      }) => {
        list.value.push({
          status: i.status,
          title: i.taskName,
          describe:
            i.taskContent1 || "" + i.taskContent2 || "" + i.taskContent3 || "",
          createTime:
            i.createTime.replace("T", " ").replace("Z", "").slice(0, 16) + " ",
        });
      }
    );
    // 加载状态结束
    loading.value = false;
    finished.value = true;
  });
};
</script>

<style>
.banner {
  margin: 3vh 5vw 1vh 5vw;
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
