<template>
  <transition>
    <div class="popup" v-if="show">
      <div class="popup-content">
        <div class="slot">
          <slot @subi="a" />
        </div>
      </div>
    </div>
  </transition>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue";
const show = ref(true);
const a = (e: any) => {
  console.log(e, "ss");
};
</script>

<style>
.popup {
  position: fixed;
  background-color: rgba(0, 0, 0, 0.4);
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.popup .popup-content {
  width: 80%;
  min-height: 40vh;
  background-color: #fff;
  border-radius: 10px;

  position: static;
}

.popup .popup-content .slot {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 80%;
}

.handler {
  display: flex;
  flex-direction: row;
  margin: 0 auto;
  width: 60%;
  height: 20%;
  justify-content: space-between;
}
.handler div {
  width: 70px;
  height: 20px;
  padding: 10px;
  border-radius: 5px;
  font-weight: 600;
  cursor: pointer;
}

.handler div:nth-child(1) {
  background-color: #9d9d9d;
  color: #fff;
  box-shadow: 0 1px 2px 0 #9d9d9d;
}
.handler div:nth-child(2) {
  background-color: #07c189;
  color: #fff;
  box-shadow: 0 1px 2px 0 #07c189;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-enter-to,
.v-leave-from {
  opacity: 1;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}
</style>
