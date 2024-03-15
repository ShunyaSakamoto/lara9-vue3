<script lang="ts">
import { defineComponent, computed, reactive, toRefs } from "vue";

export default defineComponent({
  name: "App",
  setup() {
    // リアクティブなテンプレート変数をまとめて用意
    const data = reactive({
      PI: 3.14,
      radius: Math.round(Math.random() * 10),
    });
    // 円の算出プロパティを用意
    const area = computed((): number => {
      return data.radius * data.radius * data.PI;
    });
    // 半径のテンプレート変数に新しい乱数を1秒ごとに格納
    setInterval((): void => {
      data.radius = Math.round(Math.random() * 10);
    }, 1000);

    // テンプレート変数をリターン
    return {
      // data,
      ...toRefs(data),
      area,
    };
  },
});
</script>

<template>
  <div>
    <h3>setup と reactive と toRefs</h3>
    <!-- <p>半径{{ data.radius }}の円の面積を円周率{{ data.PI }}で計算すると、{{ area }}</p> -->
    <p>半径{{ radius }}の円の面積を円周率{{ PI }}で計算すると、{{ area }}</p>
  </div>
  <hr />
</template>
