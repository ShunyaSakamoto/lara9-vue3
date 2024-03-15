<script setup lang="ts">
import { computed, ref } from "vue";

const cocktailDataListInit1: Cocktail[] = [
  { id: 2345, name: "ホワイトレディ", price: 1200 },
  { id: 4412, name: "ブルーハワイ", price: 1500 },
  { id: 6792, name: "ニューヨーク", price: 1100 },
  { id: 8492, name: "マティーニ", price: 1500 },
];
const cocktailDataList1 = ref(cocktailDataListInit1);
const cocktail1500_1 = computed((): Cocktail[] => {
  // 配列のfilter()メソッドを使って新たな配列を生成
  const newList = cocktailDataList1.value.filter(
    // filter()メソッドの絞り込み条件関数
    // 引数は配列の各要素であるCocktailオブジェクト
    (cocktailItem: Cocktail): boolean => {
      // 値段が1500かどうかの結果を戻り値とする
      return cocktailItem.price == 1500;
    }
  );

  return newList;
});
interface Cocktail {
  id: number;
  name: string;
  price: number;
}

const cocktailListInit: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cocktailList = ref(cocktailListInit);
const changeCocktailList = (): void => {
  cocktailList.value = ["バラライカ", "XYZ", "マンハッタン"];
};
const addCocktailList = (): void => {
  cocktailList.value.push("ブルームーン");
};
const deleteFromCocktailList = (): void => {
  cocktailList.value.pop();
};

const whiteLadyInit: {
  id: number;
  name: string;
  price: number;
  recipe: string;
} = {
  id: 2345,
  name: "ホワイトレディ",
  price: 1200,
  recipe: "ジン30ml+コワントロー15ml+レモン果汁+15ml",
};
const whiteLady = ref(whiteLadyInit);
const changeWhiteLadyPrice = (): void => {
  whiteLady.value.price = 1500;
};

const cocktailDataListInit2 = new Map<number, Cocktail>();
cocktailDataListInit2.set(2345, { id: 2345, name: "ホワイトレディ", price: 1200 });
cocktailDataListInit2.set(4412, { id: 4412, name: "ブルーハワイ", price: 1500 });
cocktailDataListInit2.set(6792, { id: 6792, name: "ニューヨーク", price: 1100 });
cocktailDataListInit2.set(8429, { id: 8429, name: "マティーニ", price: 1500 });
const cocktailDataList2 = ref(cocktailDataListInit2);
const cocktail1500_2 = computed(
  // 算出関数、戻り値の型はMap
  (): Map<number, Cocktail> => {
    // 絞り込んだ要素を格納する新しいMapを用意
    const newList = new Map<number, Cocktail>();
    // cocktailDataList内のMapをループ処理
    cocktailDataList2.value.forEach(
      // ループの各処理内容を表す関数
      (value: Cocktail, key: number): void => {
        // カクテルの価格が1500円ならnewListに登録
        if (value.price >= 1500) {
          newList.set(key, value);
        }
      }
    );

    // 絞り込んだ新しいMapを戻り値とする
    return newList;
  }
);
const changeWhiteLadyPriceInList = (): void => {
  const whiteLady = cocktailDataList2.value.get(2345) as Cocktail;
  whiteLady.price = 1500;
};
</script>

<template>
  <div>
    <section>
      全てのカクテルリスト
      <ul>
        <li v-for="cocktailItem in cocktailDataList1" v-bind:key="'cocktailDataList1' + cocktailItem.id">
          {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
        </li>
      </ul>
    </section>
    <section>
      値段が1500円のカクテルリスト
      <ul>
        <li v-for="cocktailItem in cocktail1500_1" v-bind:key="'cocktail1500_1' + cocktailItem.id">
          {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
        </li>
      </ul>
    </section>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="(cocktailName, index) in cocktailList" v-bind:key="cocktailName">
        {{ cocktailName }}（インデックス{{ index }}）
      </li>
    </ul>
    <p>
      CocktailListを
      <button v-on:click="changeCocktailList">変更</button>
    </p>
    <p>
      CocktailListの末尾に「ブルームーン」を
      <button v-on:click="addCocktailList">追加</button>
    </p>
    <p>
      CocktailListから末尾の要素を
      <button v-on:click="deleteFromCocktailList">削除</button>
    </p>
  </div>
  <hr />

  <div>
    <dl>
      <template v-for="(value, key) in whiteLady" v-bind:key="key">
        <dt>{{ key }}</dt>
        <dd>{{ value }}</dd>
      </template>
    </dl>
    <p>
      価格を1500円に
      <button v-on:click="changeWhiteLadyPrice">変更</button>
    </p>
  </div>
  <hr />

  <div>
    <section>
      全てのカクテルリスト
      <ul>
        <li v-for="[id, cocktailItem] in cocktailDataList2" v-bind:key="'cocktailDataList2' + id">
          {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
        </li>
      </ul>
    </section>
    <section>
      値段が1500円のカクテルリスト
      <ul>
        <li v-for="[id, cocktailItem] in cocktail1500_2" v-bind:key="'cocktail1500_2' + id">
          {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
        </li>
      </ul>
    </section>
    <p>
      CocktailDataList2内のホワイトレディの価格を1500円に
      <button v-on:click="changeWhiteLadyPriceInList">変更</button>
    </p>
  </div>
</template>
