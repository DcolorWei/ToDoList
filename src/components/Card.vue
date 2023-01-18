<template>
  <div class="card-panel">
    <div class="icon">
      <img v-if="props.process.status == 2" src="@/assets/finish.gif" />
      <img v-else-if="props.process.status == 1" src="@/assets/processing.gif" />
      <img v-else src="@/assets/waiting.gif" />
    </div>
    <div class="content">
      <div class="title">{{ props.process.title }}</div>
      <div class="describe">
        {{ props.process.describe }}
      </div>
      <div class="handler">
        <img style="width: 25px" src="@/assets/more.svg" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, defineProps } from "vue";
const props = defineProps(["process"]);
</script>

<style>
.card-panel {
  width: 80%;
  min-height: 25vw;
  margin: 2% 10%;
  border: 1px solid #ffffff;
  background-color: #ffffff;
  box-shadow: 1px 3px 4px 1px rgba(0, 0, 0, 0.2);
  border-radius: 6px;

  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

.card-panel .icon {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 20%;
}

.card-panel .icon img {
  width: 35px;
}

.card-panel .content {
  min-height: 20vw;
  width: 80%;
  text-align: left;
  padding: 5% 3%;
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

.card-panel .content .handler {
  display: flex;
  justify-content: flex-end;
  bottom: 1px;
}
</style>
