<script setup lang="ts">
import { computed, ref, watch, watchEffect } from "vue";

interface Cocktail {
  id: number;
  name: string;
  price: number;
}

// カクテルリストデータを用意
const cocktailDataListInit = new Map<number, Cocktail>();
cocktailDataListInit.set(1, { id: 1, name: "ホワイトレディ", price: 1200 });
cocktailDataListInit.set(2, { id: 2, name: "ブルーハワイ", price: 1200 });
cocktailDataListInit.set(3, { id: 3, name: "ニューヨーク", price: 1200 });
cocktailDataListInit.set(4, { id: 4, name: "マティーニ", price: 1200 });
// カクテル番号のテンプレート変数を用意
const cocktailNo1 = ref(1);
// カクテル番号に対応するカクテル情報の算出プロパティを用意
const priceMsg1 = computed((): string => {
  // カクテル番号に該当するカクテルデータを取得
  const cocktail = cocktailDataListInit.get(cocktailNo1.value);
  // カクテル番号に該当する情報がない場合のメッセージを用意
  let msg = "該当カクテルはありません。";
  // カクテル番号に該当する情報があるなら
  if (cocktail != undefined) {
    // カクテル番号に該当するカクテルの名前と金額を表示する文字列を生成
    msg = `該当するカクテルは${cocktail.name}で、価格は${cocktail.price}円です。`;
  }

  // 表示文字列をリターン
  return msg;
});
// cocktailNo1を1秒ごとに1〜4の乱数を使って変更
setInterval((): void => {
  cocktailNo1.value = Math.round(Math.random() * 3) + 1;
}, 1000);

// カクテル番号のテンプレート変数を用意
const cocktailNo2 = ref(1);
// カクテル番号に対応するカクテル情報のテンプレート変数を用意
const priceMsg2 = ref("");
// watchEffect2を設定
watchEffect((): void => {
  priceMsg2.value = getCocktailInfo(cocktailNo2.value);
});
// cocktailNoを1秒ごとに1〜4の乱数を使って変更
setInterval((): void => {
  cocktailNo2.value = Math.round(Math.random() * 3) + 1;
}, 1000);
// カクテル番号に対応するカクテル情報を取得する関数
function getCocktailInfo(cocktailNo: number): string {
  const cocktailDataListInit = new Map<number, Cocktail>();
  cocktailDataListInit.set(1, { id: 1, name: "ホワイトレディ", price: 1200 });
  cocktailDataListInit.set(2, { id: 2, name: "ブルーハワイ", price: 1200 });
  cocktailDataListInit.set(3, { id: 3, name: "ニューヨーク", price: 1200 });
  cocktailDataListInit.set(4, { id: 4, name: "マティーニ", price: 1200 });
  // カクテル番号に該当するカクテルデータを取得
  const cocktail = cocktailDataListInit.get(cocktailNo);
  // カクテル番号に該当する情報がない場合のメッセージを用意
  let msg = "該当カクテルはありません。";
  // カクテル番号に該当する情報があるなら
  if (cocktail != undefined) {
    // カクテル番号に該当するカクテルの名前と金額を表示する文字列を生成
    msg = `該当するカクテルは${cocktail.name}で、価格は${cocktail.price}円です。`;
  }

  // 表示文字列をリターン
  return msg;
}

// カクテル番号のテンプレート変数を用意
const cocktailNo3 = ref(1);
// カクテル番号に対応するカクテル情報のテンプレート変数を用意
const priceMsg3 = ref("");
watch(cocktailNo3, (): void => {
  priceMsg3.value = getCocktailInfo(cocktailNo3.value);
});
// cocktailNo3を1秒ごとに1〜4の乱数を使って変更
setInterval((): void => {
  cocktailNo3.value = Math.round(Math.random() * 3) + 1;
}, 1000);

// カクテル番号のテンプレート変数を用意
const cocktailNo4 = ref(1);
// カクテル番号に対応するカクテル情報のテンプレート変数を用意
const priceMsg4 = ref("");
watch(
  cocktailNo4,
  (): void => {
    priceMsg4.value = getCocktailInfo(cocktailNo4.value);
  },
  { immediate: true }
);
// cocktailNo4を1秒ごとに1〜4の乱数を使って変更
setInterval((): void => {
  cocktailNo4.value = Math.round(Math.random() * 3) + 1;
}, 1000);

// カクテル番号のテンプレート変数を用意
const cocktailNo5 = ref(1);
// カクテル番号に対応するカクテル情報のテンプレート変数を用意
const priceMsg5 = ref("");
watch(cocktailNo5, (newVal: number, oldVal: number): void => {
  // 表示用文字列を用意
  let msg = "前のカクテル: ";
  msg += getCocktailInfo(oldVal);
  msg += "現在のカクテル: ";
  msg += getCocktailInfo(newVal);
  // 表示用ボジ列をpriceMsg4に設定
  priceMsg5.value = msg;
});
// cocktailNo5を1秒ごとに1〜4の乱数を使って変更
setInterval((): void => {
  cocktailNo5.value = Math.round(Math.random() * 3) + 1;
}, 5000);
</script>

<template>
  <div>
    <h3>算出プロパティの役割</h3>
    <p>現在のカクテル番号: {{ cocktailNo1 }}</p>
    <p>{{ priceMsg1 }}</p>
  </div>
  <hr />

  <div>
    <h3>リアクティブ変数の変化を監視する watchEffect()</h3>
    <p>現在のカクテル番号: {{ cocktailNo2 }}</p>
    <p>{{ priceMsg2 }}</p>
  </div>
  <hr />

  <div>
    <h3>監視対象を明示する watch()</h3>
    <p>現在のカクテル番号: {{ cocktailNo3 }}</p>
    <p>{{ priceMsg3 }}</p>
  </div>
  <hr />

  <div>
    <h3>即時実行の watch()</h3>
    <p>現在のカクテル番号: {{ cocktailNo4 }}</p>
    <p>{{ priceMsg4 }}</p>
  </div>
  <hr />

  <div>
    <h3>watch() における変更前後の値の利用</h3>
    <p>現在のカクテル番号: {{ cocktailNo5 }}</p>
    <p>{{ priceMsg5 }}</p>
  </div>
</template>
