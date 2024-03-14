<script setup lang="ts">
import { ref } from "vue";

const cocktailListInit1: string[] = ["ホワイトレディ", "ブルーハワイ", "ニューヨーク"];
const cocktailList1 = ref(cocktailListInit1);

const cocktailListInit2: { [key: number]: string } = {
  2345: "ホワイトレディ",
  4412: "ブルーハワイ",
  6792: "ニューヨーク",
};
const cocktailList2 = ref(cocktailListInit2);

const cocktailListInit3 = new Map<number, string>();
cocktailListInit3.set(2345, "ホワイトレディ");
cocktailListInit3.set(4412, "ブルーハワイ");
cocktailListInit3.set(6792, "ニューヨーク");
const cocktailList3 = cocktailListInit3;

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

const cocktailDataListInit1: Cocktail[] = [
  { id: 2345, name: "ホワイトレディ", price: 1200 },
  { id: 4412, name: "ブルーハワイ", price: 1500 },
  { id: 6792, name: "ニューヨーク", price: 1100 },
  { id: 8429, name: "マティーニ", price: 1500 },
];
const cocktailDataList1 = ref(cocktailDataListInit1);
interface Cocktail {
  id: number;
  name: string;
  price: number;
}

const cocktailDataListInit2 = new Map<number, Cocktail>();
cocktailDataListInit2.set(2345, { id: 2345, name: "ホワイトレディ", price: 1200 });
cocktailDataListInit2.set(4412, { id: 4412, name: "ブルーハワイ", price: 1500 });
cocktailDataListInit2.set(6792, { id: 6792, name: "ニューヨーク", price: 1100 });
cocktailDataListInit2.set(8492, { id: 8492, name: "マティーニ", price: 1500 });
const cocktailDataList2 = ref(cocktailDataListInit2);
</script>

<template>
  <div>
    <ul>
      <li v-for="cocktailName in cocktailList1" v-bind:key="cocktailName">{{ cocktailName }}</li>
    </ul>
    <ul>
      <li v-for="(cocktailName, index) in cocktailList1" v-bind:key="cocktailName">
        {{ cocktailName }}（インデックス{{ index }}）
      </li>
    </ul>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="(cocktailName, id) in cocktailList2" v-bind:key="'cocktailList' + id">
        IDが{{ id }}のカクテルは{{ cocktailName }}
      </li>
    </ul>
    <ul>
      <li v-for="(cocktailName, id, index) in cocktailList2" v-bind:key="'cocktailListWithIdx' + id">
        {{ index + 1 }}: IDが{{ id }}のカクテルは{{ cocktailName }}
      </li>
    </ul>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="[id, cocktailName] in cocktailList3" v-bind:key="id">IDが{{ id }}のカクテルは{{ cocktailName }}</li>
    </ul>
  </div>
  <hr />

  <div>
    <dl>
      <template v-for="(value, key) in whiteLady" v-bind:key="key">
        <dt>{{ key }}</dt>
        <dd>{{ value }}</dd>
      </template>
    </dl>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="cocktailItem in cocktailDataList1" v-bind:key="cocktailItem.id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="[id, cocktailItem] in cocktailDataList2" v-bind:key="id">
        {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
      </li>
    </ul>
  </div>
  <hr />

  <div>
    <ul>
      <li v-for="r in 5" v-bind:key="r">半径{{ r }}の円の円周: {{ 2 * r * 3.14 }}</li>
    </ul>
    <select>
      <option v-for="year in 60" v-bind:key="year" v-bind:value="year + 1965">{{ year + 1965 }}</option>
    </select>
  </div>
</template>
