<script setup lang="ts">
import { ref } from "vue";

const htmlStr = ref(`<a href="https://vuejs.org//">VueElement.jsのTOPページ</a>`);

const price = ref(1000);

const hello = ref("hello!");
</script>

<template>
  <div>
    <section>{{ htmlStr }}</section>
    <section v-html="htmlStr"></section>
  </div>
  <hr />

  <div>
    <section v-pre>
      <p v-on:click="showHello">{{ hello! }}</p>
    </section>
  </div>
  <hr />

  <div>
    <section>
      <input type="number" v-model="price" />円
      <br />
      <p>金額は{{ price }}円です。</p>
      <p v-once>金額は{{ price }}です。</p>
    </section>
  </div>
  <hr />

  <div>
    <p v-cloak>{{ hello }}</p>
  </div>
</template>

<style>
[v-cloak] {
  display: none;
}
</style>
