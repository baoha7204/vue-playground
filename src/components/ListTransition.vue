<script setup>
import { ref } from "vue";
const props = defineProps({
  initialItems: Array,
});
import { shuffle as _shuffle } from "lodash";
const getInitialItems = () => props.initialItems;
const items = ref(getInitialItems());
const nextNum = ref(items.value.length);

const randomIndex = () => Math.floor(Math.random() * items.value.length);
const add = () => items.value.splice(randomIndex(), 0, nextNum.value++);
const remove = () => items.value.splice(randomIndex(), 1);
const reset = () => (items.value = getInitialItems());
const shuffle = () => (items.value = _shuffle(items.value));
</script>

<template>
  <div>
    <div class="flex gap-2">
      <button @click="shuffle">Shuffle</button>
      <button @click="add">Add</button>
      <button @click="remove">Remove</button>
      <button @click="reset">Reset</button>
    </div>
    <transition-group name="list" tag="p">
      <span v-for="item in items" :key="item" class="inline-block mr-2">
        {{ item }}
      </span>
    </transition-group>
  </div>
</template>

<style>
.list-move {
  transition: transform 1s;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>
