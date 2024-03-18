<script setup lang="ts">
import { computed, ref } from "vue";
import OneMember from "./components/OneMember.vue";
import OneSection from "./components/OneSection.vue";

// 会員情報インターフェイス
interface Member {
  id: number;
  name: string;
  email: string;
  points: number;
  note?: string;
}

const randInit = Math.round(Math.random() * 10);
const rand = ref(randInit);
const onCreateNewRand = (): void => {
  rand.value = Math.round(Math.random() * 10);
};

// 会員リスト用意
const memberListInit = new Map<number, Member>();
memberListInit.set(33456, {
  id: 33456,
  name: "田中太郎",
  email: "bow@example.com",
  points: 35,
  note: "初回入会特典あり。",
});
memberListInit.set(47783, { id: 47783, name: "鈴木二郎", email: "mue@example.com", points: 53 });
const memberList = ref(memberListInit);
// 会員リスト内の全会員のポイント合計の算出プロパティ
const totalPoints = computed((): number => {
  let total = 0;
  for (const member of memberList.value.values()) {
    total += member.points;
  }

  return total;
});
// Emitより実行されるメソッド
// const onIncrementPoint = (id: number): void => {
//   // 処理関数のidに該当する会員情報オブジェクトを取得
//   const member = memberList.value.get(id);
//   // 会員情報オブジェクトが存在するなら
//   if (member != undefined) {
//     // ポイントをインクリメント
//     member.points++;
//   }
// };
</script>

<template>
  <section>
    <p>親コンポーネントで乱数を表示</p>
    <OneSection v-bind:rand="rand" v-on:createNewRand="onCreateNewRand" />
  </section>
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイントの合計: {{ totalPoints }}</p>
    <!-- <OneMember
      v-for="[id, member] in memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-bind:points="member.points"
      v-bind:note="member.note"
      v-on:incrementPoint="onIncrementPoint"
    /> -->
    <OneMember
      v-for="[id, member] in memberList"
      v-bind:key="id"
      v-bind:id="id"
      v-bind:name="member.name"
      v-bind:email="member.email"
      v-model:points="member.points"
      v-bind:note="member.note"
    />
  </section>
</template>
