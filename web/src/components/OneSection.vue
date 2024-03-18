<script setup lang="ts">
import { defineEmits, defineProps } from "vue";

interface Props {
  rand: number;
}

interface Emits {
  (event: "createNewRand"): void;
}

defineProps<Props>();
const emit = defineEmits<Emits>();
const onNewRandButtonClick = (): void => {
  emit("createNewRand");
};
</script>

<template>
  <section class="box">
    <h3>子から親への通信はイベント処理</h3>
    <p>子コンポーネントで乱数を表示: {{ rand }}</p>
    <button v-on:click="onNewRandButtonClick">新たな乱数を発生</button>
  </section>
</template>

<style scoped>
.box {
  border: green 1px solid;
  margin: 10px;
}
</style>
