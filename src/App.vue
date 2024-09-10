<script setup>
import { useDark, useDateFormat, useNow, useToggle } from "@vueuse/core";

const formatted = useDateFormat(useNow(), "MM-DD-YYYY HH:mm:ss");

const isDark = useDark({
  disableTransition: false,
});

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
</template>
