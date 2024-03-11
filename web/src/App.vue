<script setup lang="ts">
import { computed, reactive, ref } from "vue";

/* リアクティブデータ */

const now = new Date();

// 現在の時刻の文字列を取得
const nowStr = now.toLocaleTimeString();
let timeStr = nowStr;
const timeStrRef = ref(nowStr);

function changeTime(): void {
  const newTime = new Date();
  const newTimeStr = newTime.toLocaleTimeString();
  timeStr = newTimeStr;
  timeStrRef.value = newTimeStr;
}
// changeTime関数を1秒ごとに実行
setInterval(changeTime, 1000);

/* 算出プロパティ */

// リアクティブデータをまとめて定義する
const data = reactive({
  PI: 3.14,
  radius: Math.round(Math.random() * 10),
});

const area = computed((): number => {
  return data.radius * data.radius * data.PI;
});

// const radiusInit = Math.round(Math.random() * 10);
// const PI = ref(3.14);
// const radius = ref(radiusInit);
// const area = computed((): number => {
//   return radius.value * radius.value * PI.value;
// });

// 半径のテンプレート変数に新しい乱数を1秒ごとに格納
setInterval((): void => {
  data.radius = Math.round(Math.random() * 10);
}, 3000);
// setInterval((): void => {
//   radius.value = Math.round(Math.random() * 10);
// }, 3000);
</script>

<template>
  <div>
    <h3>リアクティブデータ</h3>
    <p>現在時刻: {{ timeStr }}</p>
    <p>現在時刻(ref): {{ timeStrRef }}</p>
  </div>
  <div>
    <h3>算出プロパティ</h3>
    <p>
      半径{{ data.radius }}の円の面積を円周率{{ data.PI }}で計算すると、{{
        area
      }}
    </p>
  </div>
</template>
