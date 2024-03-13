<script setup lang="ts">
import { ref } from "vue";

const randValue = ref("まだです");
const onButtonClick = (): void => {
  const rand = Math.round(Math.random() * 10);
  randValue.value = String(rand);
};

const mousePointerX = ref(0);
const mousePointerY = ref(0);
const onImgMousemove = (event: MouseEvent): void => {
  mousePointerX.value = event.offsetX;
  mousePointerY.value = event.offsetY;
};

const pBgColor = ref("white");
const onPClick = (bgColor: string): void => {
  pBgColor.value = bgColor;
};

const pMsg = ref("イベント前(ここをクリック！)");
const pBgColorEvent = ref("white");
const onPClickWithEvent = (bgColor: string, event: MouseEvent): void => {
  pBgColorEvent.value = bgColor;
  pMsg.value = event.timeStamp.toString();
};

const sendMsg = ref("未送信");
const onFormSubmit = (): void => {
  sendMsg.value = "送信されました。";
};

const msg = ref("まだです。");
const onEnterKey = (): void => {
  msg.value = "エンターキーが押下されました。";
};
const onRightButtonClick = (): void => {
  msg.value = "ボタンが右クリックされました。";
};
const onShiftClick = (): void => {
  msg.value = "シフトを押しながらクリックされました。";
};
</script>

<template>
  <div>
    <h3>イベントリスナを設定するディレクティブ v-on</h3>
    <section>
      <button v-on:click="onButtonClick">クリック</button>
      <p>クリック結果: {{ randValue }}</p>
    </section>
  </div>
  <hr />

  <div>
    <h3>メソッドを引数としてイベントオブジェクトを受け取る</h3>
    <section>
      <img src="./assets/logo.png" alt="Vueのロゴ" width="200" v-on:mousemove="onImgMousemove" />
      <p>ポインタの位置: x={{ mousePointerX }}; y={{ mousePointerY }}</p>
    </section>
  </div>
  <hr />

  <div>
    <h3>イベントオブジェクト以外を引数とするイベントハンドラメソッド</h3>
    <p v-on:click="onPClick('red')" v-bind:style="{ backgroundColor: pBgColor }">
      ここをクリックすると背景色が変わります。
    </p>
  </div>
  <hr />

  <div>
    <h3>イベントオブジェクトとその他の引数を併用するイベントハンドラメソッド</h3>
    <p v-on:click="onPClickWithEvent('green', $event)" v-bind:style="{ backgroundColor: pBgColorEvent }">
      {{ pMsg }}
    </p>
  </div>
  <hr />

  <div>
    <h3>v-onの修飾子 prevent修飾子</h3>
    <form action="#" v-on:submit.prevent="onFormSubmit">
      <input type="text" required />
      <button type="submit">送信</button>
    </form>
    <p>{{ sendMsg }}</p>
  </div>
  <hr />

  <div>
    <h3>クリックイベントとキーイベントの修飾子</h3>
    <p>{{ msg }}</p>
    <input type="text" v-on:keydown.enter="onEnterKey" /><br />
    <button v-on:click.right="onRightButtonClick">右クリック</button><br />
    <button v-on:click.shift="onShiftClick">シフトを押しながらクリック</button><br />
  </div>
</template>
