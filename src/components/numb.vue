<template>
  <div>
    Type a number: <input v-model.number="number" />
    <p>{{ tweened.number.toFixed(0) }}</p>
  </div>
</template>

<script>
import { ref, reactive, watch } from 'vue';
import gsap from 'gsap';

export default {
  setup() {
    const number = ref(0);
    const tweened = reactive({
      number: 0
    });

    watch(
      number,
      (n) => {
        gsap.to(tweened, { duration: 0.9, number: Number(n) || 0 });
      }
    );

    return { number, tweened };
  }
};
</script>

<style>
.big-number {
  font-weight: bold;
  font-size: 2em;
}
</style>
