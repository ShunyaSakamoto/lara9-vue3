<script setup lang="ts">
import { computed, ref } from "vue";

const number = ref(80);
const showOrNot = computed((): boolean => {
  // 戻り値変数を初期値falseで用意
  let showOrNot = false;
  // 0〜100の乱数を発生
  const rand = Math.round(Math.random() * 100);
  // 乱数が50以上ならば、戻り値をtrueに変更
  if (rand >= 50) {
    showOrNot = true;
  }

  return showOrNot;
});

const randomNumber = computed((): number => {
  return Math.round(Math.random() * 100);
});
</script>

<template>
  <div>
    <p v-if="number >= 50">条件に合致したので表示①</p>
    <p v-if="Math.round(Math.random() * 100) >= 50">条件に合致したので表示②</p>
    <p v-if="showOrNot">条件に合致したので表示③</p>
  </div>
  <hr />

  <div>
    <p>
      点数は{{ randomNumber }}点で
      <span v-if="randomNumber >= 80">優です。</span>
      <span v-else-if="randomNumber >= 70">良です。</span>
      <span v-else-if="randomNumber >= 60">可です。</span>
      <span v-else>不可です。</span>
    </p>
  </div>
  <hr />

  <div>
    <p>
      点数は{{ randomNumber }}点
      <template v-if="randomNumber >= 80">
        で優です。
        <span style="color: red">すばらしい!</span>
      </template>
    </p>
  </div>
  <hr />

  <div>
    <section>
      v-ifを利用
      <p v-if="showOrNot">条件に合致したので表示</p>
    </section>
    <section>
      v-showを利用
      <p v-show="showOrNot">条件に合致したので表示</p>
    </section>
  </div>
</template>
