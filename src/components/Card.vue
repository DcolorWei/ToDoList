<template>
  <div class="card-panel">
    <div class="icon">
      <img v-if="props.process.status == 2" src="@/assets/finish.gif" />
      <img
        v-else-if="props.process.status == 1"
        src="@/assets/processing.gif"
      />
      <img v-else src="@/assets/waiting.gif" />
    </div>
    <div class="content">
      <div class="title">{{ props.process.title }}</div>
      <div class="describe">
        {{ props.process.describe }}
      </div>
      <div class="handle">
        <Popover
          v-model:show="showPopover"
          :actions="[{ text: '编辑' }, { text: '编辑' }]"
          @select="() => {}"
        >
          <template #reference>
            <div @click="showPopoverFunc()">
              <img style="width: 25px" src="@/assets/more.svg" />
            </div>
          </template>
        </Popover>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, defineProps } from "vue";
import { Popover } from "vant";
const props = defineProps(["process"]);
const showPopover = ref(false);
function showPopoverFunc() {
  console.log("s");
  showPopover.value = true;
}
</script>

<style>
.card-panel {
  width: 80%;
  min-height: 20vh;
  margin: 2% 10%;
  border: 1px solid #f8f9fd;
  background-color: #f8f9fd;
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
  min-height: 10vh;
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

.card-panel .content .handle {
  display: flex;
  justify-content: flex-end;
  bottom: 1px;
}
</style>
