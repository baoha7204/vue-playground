<script>
import gsap from "gsap";
export default {
  data() {
    return {
      number: 0,
      tweenedNumber: 0,
    };
  },
  computed: {
    animatedNumber() {
      return this.tweenedNumber.toFixed(0);
    },
  },
  watch: {
    number(newValue) {
      gsap.to(this.$data, { duration: 0.5, tweenedNumber: newValue });
    },
  },
  directives: {
    focus: {
      mounted(el) {
        el.focus();
      },
    },
  },
};
</script>

<template>
  <input v-focus v-model.number="number" type="number" step="25" />
  <p>{{ animatedNumber }}</p>
</template>
