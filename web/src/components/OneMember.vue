<script setup lang="ts">
import { computed, defineEmits, defineProps } from "vue";

// Propsインターフェイスの定義
interface Props {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

// Emitインターフェイスの定義
interface Emits {
  (event: "incrementPoint", id: number): void;
  (event: "update:points", points: number): void;
}

//Propsオブジェクトの設定
const props = defineProps<Props>();
// Emitの設定
const emit = defineEmits<Emits>();
// Propsのnoteを加工する算出プロパティ
const localNote = computed((): string => {
  let localNote = props.note;
  if (localNote == undefined) {
    localNote = "--";
  }

  return localNote;
});
// [ポイント加算]ボタンをクリックしたときのメソッド
// const pointUp = (): void => {
//   emit("incrementPoint", props.id);
// };

const onInput = (event: Event): void => {
  const element = event.target as HTMLInputElement;
  const inputPoints = Number(element.value);
  emit("update:points", inputPoints);
};
</script>

<template>
  <section class="box">
    <h4>{{ name }}さんの情報</h4>
    <dl>
      <dt>ID</dt>
      <dd>{{ id }}</dd>
      <dt>メールアドレス</dt>
      <dd>{{ email }}</dd>
      <dt>保有ポイント</dt>
      <!-- <dd>{{ points }}</dd> -->
      <dd><input type="number" v-bind:value="points" v-on:input="onInput" /></dd>
      <dt>備考</dt>
      <dd>{{ localNote }}</dd>
    </dl>
    <!-- <button v-on:click="pointUp">ポイント加算</button> -->
  </section>
</template>

<style scoped>
.box {
  border: green 1px solid;
  margin: 10px;
}
</style>
