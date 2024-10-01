<script setup>
import { useDark, useDateFormat, useNow, useToggle } from "@vueuse/core";
import { ref } from "vue";
// import ListTransition from "./components/ListTransition.vue";
import StateTransition from "./components/StateTransition.vue";

const formatted = useDateFormat(useNow(), "DD/MM/YYYY HH:mm:ss");

const isDark = useDark({
  disableTransition: false,
});
const show = ref(true);
const toggleDark = useToggle(isDark);
</script>

<template>
  <div
    class="bg-white text-slate-800 dark:bg-slate-800 dark:text-white flex flex-col items-center m-10 gap-10"
  >
    <button class="bg-green-300 p-2 font-semibold" @click="toggleDark()">
      Switch mode
    </button>
    <h1 class="text-3xl">{{ formatted }}</h1>
  </div>
  <div>
    <button class="bg-black text-white" @click="show = !show">
      Toggle transition
    </button>
    <transition name="fade"><p v-if="show">Transition ...</p> </transition>
  </div>
  <br />
  <StateTransition />
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
