<script setup>
import { computed, reactive, ref, toRefs } from "vue";

defineProps({
  msg: String,
});

const count = ref(0);
const plusOne = computed(() => count.value + 1);
console.log("plusOne：" + plusOne.value);
plusOne.value++; // 错误
const plusOne1 = computed({
  get: () => count.value + 1,
  set: (val) => {
    count.value = val - 1;
  },
});
plusOne1.value = 5;
console.log(count.value);
</script>

<template>
  <h1>{{ msg }}</h1>
  <button @click="count++">{{ count }}</button>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
