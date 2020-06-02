<template>
  <div class="calc">
    <label>
      <input type="radio" name="sex" value="1" />男性
    </label>
    <label>
      <input type="radio" name="sex" value="2" />女性
    </label>
    <input type="text" placeholder="体重" />
    <input type="text" placeholder="身長" />
    <input type="text" placeholder="年齢" />
    <h2>基礎代謝</h2>

    <h3>男性</h3>
    <p>10×体重（kg）＋6.25×身長（cm)－5×年齢（歳）＋5＝基礎代謝</p>
    <h3>女性</h3>

    <p>
      10×体重（kg）＋6.25×身長（cm)－5×年齢（歳）＋5＝基礎代謝
      <br />170cm・60kg・35歳 男性の場合
      <br />10×60（kg）＋6.25×170（cm）－5×35（歳）＋5＝1492.5
    </p>

    <h2>消費カロリー</h2>
    <h3>活動量</h3>

    <label>
      <input type="radio" name="workLevel" value="1" />アクティブ度が低い人（基礎代謝×1.2）
      <br />座り仕事が多く、1日の運動は歩いたり階段を上ったりする程度
    </label>
    <label>
      <input type="radio" name="workLevel" value="1" />アクティブ度がまあまあ高い人（基礎代謝×1.55）
      <br />立ち仕事や重労働が多く、比較的一日中動き回っている
    </label>
    <label>
      <input type="radio" name="workLevel" value="1" />アクティブ度が高い人（基礎代謝×1.725）
      <br />立ち仕事や重労働が多く、加えてジムでのトレーニングや運動をしている
    </label>
    <p>
      170cm・60kg・35歳・男性・アクティブ度が高い場合の例
      <br />基礎代謝＝1492.5（STEP1で計算した値）
      <br />1日の消費カロリー＝1492.5×1.725＝2574.6kcal（小数点第2位以下四捨五入）
    </p>

    <h2>目標摂取カロリー</h2>
    <p>
      ・増量、筋肉を増やしたい人は「1日の消費カロリー」×1.2
      <br />・ひとまず現状を維持したい人は「1日の消費カロリー」×1
      <br />・引き締め・ダイエットしたい人は「1日の消費カロリー」×0.8
      <br />170cm・60kg・35歳・男性・アクティブ度が高い・減量したい場合の例
      <br />2574.6kcal（STEP2で出した1日の消費カロリー）×0.8＝2059kcal
    </p>

    <h2>目標栄養素量とバランス</h2>
    <p>タンパク質は倍、脂質は総摂取カロリーの２５％、残りが炭水化物</p>
    <blockquote>https://dietgenius.jp/macro-nutrient-calculator/</blockquote>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Calc extends Vue {}
</script>

<style scoped lang="scss">
.calc {
  background-color: #fafafa;
  border: 1px solid #eee;
}
</style>
