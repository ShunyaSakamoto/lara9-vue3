<script setup lang="ts">
import { ref, computed } from "vue";

const url = ref("https://vuejs.org/");

const isSendButtonDisabled = ref(true);

const widthOrHeight = ref("height");
const widthOrHeightValue = ref(100);

const imgAttributes = ref({
  src: "/images/logo.svg",
  alt: "Vueのロゴ",
  width: 75,
  height: 75,
});

const msg = ref("Hello world!");
const msgTextRed = ref("red");
const msgTextColor = ref("white");
const msgBgColor = ref("black");
const msgStyles1 = ref({
  color: "white",
  backgroundColor: "black",
});
const msgStyles2 = ref({
  fontSize: "24pt",
});
const msgStyles3 = ref({
  color: "pink",
  fontSize: "24pt",
});
const textSize = computed((): string => {
  const size = Math.round(Math.random() * 25) + 10;

  return `${size}pt`;
});

const isTextColorRed = ref(true);
const isBgColorBlue = ref(false);
const styles = ref({
  textColorRed: false,
  bgColorBlue: true,
});
const computedStyles = computed((): { textColorRed: boolean; bgColorBlue: boolean } => {
  // 乱数を利用して0か1を生成（textColorRed用）
  const randText = Math.round(Math.random());
  // textColorRedプロパティの値を表す変数をtrueで用意
  let textColorFlg = true;
  // 発生した乱数が0ならばfalseに変更
  if (randText == 0) {
    textColorFlg = false;
  }

  // 乱数を利用して0か1を生成（bgColorBlue用）
  const randBg = Math.round(Math.random());
  // bgColorBlueプロパティの値を表す変数をtrueで用意
  let bgColorFlg = true;
  // 発生した乱数が0ならばfalseに変更
  if (randBg == 0) {
    bgColorFlg = false;
  }
  // それぞれのプロパティの値をオブジェクトにして返す
  return {
    textColorRed: textColorFlg,
    bgColorBlue: bgColorFlg,
  };
});
</script>

<template>
  <div>
    <h3>属性にデータバインドするv-bind</h3>
    <p><a v-bind:href="url" target="_blank">Vue.jsのサイト</a></p>
    <p><a :href="url" target="_blank">Vue.jsのサイト（省略形）</a></p>
    <p><a :href="url + 'guide/introduction.html'" target="_blank">Vue.jsガイドのページ</a></p>
  </div>
  <hr />

  <div>
    <h3>属性値のない属性へのバインド</h3>
    <p><button type="button" :disabled="isSendButtonDisabled">送信</button></p>
  </div>
  <hr />

  <div>
    <h3>バインドする属性をテンプレート変数として指定</h3>
    <p><img src="./assets/logo.png" alt="VueLogo" height="100" :[widthOrHeight]="widthOrHeightValue" /></p>
  </div>
  <hr />

  <div>
    <h3>複数の属性にまとめてバインドする方法</h3>
    <p><img v-bind="imgAttributes" /></p>
    <p><img v-bind="imgAttributes" title="ロゴです！" /></p>
    <p><img v-bind="imgAttributes" alt="ロゴです！" /></p>
    <!-- imgAttributesオブジェクトのaltプロパティに上書きされる -->
    <p><img alt="ロゴです！" v-bind="imgAttributes" /></p>
  </div>
  <hr />

  <div>
    <h3>style属性へのバインディング</h3>
    <p :style="{ color: msgTextRed }">{{ msg }}</p>
    <p :style="{ color: 'pink' }">{{ msg }}</p>
    <p :style="{ fontSize: textSize }">{{ msg }}</p>
    <p :style="{ color: msgTextColor, backgroundColor: msgBgColor }">{{ msg }}</p>
    <p :style="{ color: msgTextColor, 'background-color': msgBgColor }">{{ msg }}</p>
    <p :style="msgStyles1">{{ msg }}</p>
    <p :style="[msgStyles1, msgStyles2]">{{ msg }}</p>
    <p :style="[msgStyles1, msgStyles3]">{{ msg }}</p>
    <p :style="[msgStyles3, msgStyles1]">{{ msg }}</p>
  </div>
  <hr />

  <div>
    <h3>class属性へのバインディング</h3>
    <p :class="{ textColorRed: true, bgColorBlue: true }">{{ msg }}</p>
    <p :class="{ textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue }">{{ msg }}</p>
    <p :class="{ textColorPink: true }">{{ msg }}</p>
    <p :class="{ 'text-color-pink': true }">{{ msg }}</p>
    <p class="textSize24" :class="{ textColorRed: isTextColorRed, bgColorBlue: isBgColorBlue }">{{ msg }}</p>
    <p class="textSize24" :class="styles">{{ msg }}</p>
    <p :class="computedStyles">{{ msg }}</p>
  </div>
</template>

<style>
.textColorRed {
  color: red;
}
.text-color-pink {
  color: pink;
}
.bgColorBlue {
  background-color: blue;
}
.textSize24 {
  font-size: 24px;
}
</style>
