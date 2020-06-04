<template>
  <div class="calcs">
    <section>
      <h2>性別</h2>
      <label>
        <input type="radio" name="sex" value="male" v-model="sex" />
        男性
      </label>
      <label>
        <input type="radio" name="sex" value="female" v-model="sex" />
        女性
      </label>
    </section>
    <div>
      <section>
        <h2>体重</h2>
        <input type="text" name="weight" v-model="weight" /> kg
      </section>
      <section>
        <h2>身長</h2>
        <input type="text" name="height" v-model="height" /> cm
      </section>
      <section>
        <h2>年齢</h2>
        <input type="text" name="age" placeholder="年齢" v-model="age" />
      </section>
    </div>

    <h2>基礎代謝</h2>
    <p>{{ bmr }} (kcal / day)</p>

    <h3>男性</h3>
    <p>BMR (kcal / day) = 10 * weight (kg) + 6.25 * height (cm) – 5 * age (y) + 5 (kcal / day)</p>
    <h3>女性</h3>
    <p>BMR (kcal / day)= 10 x weight (kg) + 6.25 x height (cm) – 5 x age (y) – 161 (kcal / day)</p>

    <h2>消費カロリー</h2>
    <p>{{ calorieConsumption }} (kcal / day)</p>
    <h3>活動量</h3>
    <div>
      <label>
        <input type="radio" name="activity" value="low" v-model="activity" />アクティブ度が低い人（基礎代謝×1.2）
        <br />座り仕事が多く、1日の運動は歩いたり階段を上ったりする程度
      </label>
    </div>
    <div class>
      <label>
        <input type="radio" name="activity" value="middle" v-model="activity" />アクティブ度がまあまあ高い人（基礎代謝×1.55）
        <br />立ち仕事や重労働が多く、比較的一日中動き回っている
      </label>
    </div>
    <div>
      <label>
        <input type="radio" name="activity" value="high" v-model="activity" />アクティブ度が高い人（基礎代謝×1.725）
        <br />立ち仕事や重労働が多く、加えてジムでのトレーニングや運動をしている
      </label>
    </div>

    <h2>目標摂取カロリー</h2>
    <p>{{ consumedCalories }} (kcal / day)</p>
    <div>
      <label>
        <input type="radio" name="goal" value="gain" v-model="goal" /> 増量、筋肉を増やしたい人は「1日の消費カロリー」×1.2
      </label>
    </div>
    <div>
      <label>
        <input type="radio" name="goal" value="keep" v-model="goal" /> ひとまず現状を維持したい人は「1日の消費カロリー」×1
      </label>
    </div>
    <div>
      <label>
        <input type="radio" name="goal" value="slim" v-model="goal" /> 引き締め・ダイエットしたい人は「1日の消費カロリー」×0.8
      </label>
    </div>

    <h2>目標栄養素量とバランス</h2>
    <p>タンパク質は倍、脂質は総摂取カロリーの２５％、残りが炭水化物</p>
    <p>Protein（タンパク質） : {{ intakeProtein }}g / {{ intakeProteinCalories }}kcal (day)</p>
    <p>Fat（脂質） : {{ intakeFat }}g / {{ intakeFatCalories }}kcal (day)</p>
    <p>Carbo（炭水化物） : {{ intakeCarbo }}g / {{ intakeCarboCalories }}kcal (day)</p>

    <blockquote>
      https://dietgenius.jp/macro-nutrient-calculator/
      <br />https://www.omnicalculator.com/health/bmr
    </blockquote>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class Calcs extends Vue {
  sex = "male";
  weight = 78;
  height = 178;
  age = 28;
  activity = "low";
  goal = "slim";

  get bmr() {
    return (
      10 * this.weight + 6.25 * this.height - 5 * this.age + this.sexCoefficient
    );
  }

  get calorieConsumption() {
    return Math.round(this.bmr * this.activityCoefficient);
  }

  get consumedCalories() {
    return Math.round(this.calorieConsumption * this.goalCoefficient);
  }

  get sexCoefficient() {
    return this.sex == "male" ? 5 : -161;
  }

  get activityCoefficient() {
    switch (this.activity) {
      case "low":
        return 1.2;
      case "middle":
        return 1.55;
      case "high":
        return 1.725;
      default:
        return 1;
    }
  }

  get goalCoefficient() {
    switch (this.goal) {
      case "gain":
        return 1.2;
      case "keep":
        return 1;
      case "slim":
        return 0.8;
      default:
        return 1;
    }
  }

  get intakeProtein() {
    return this.weight * 2;
  }
  get intakeFat() {
    return Math.round((this.consumedCalories * 0.25) / 9);
  }
  get intakeCarbo() {
    return Math.round(
      (this.consumedCalories - this.intakeFat * 9 - this.intakeProtein * 4) / 4
    );
  }

  get intakeProteinCalories() {
    return this.weight * 2 * 4;
  }
  get intakeFatCalories() {
    return Math.round(this.consumedCalories * 0.25);
  }
  get intakeCarboCalories() {
    return Math.round(
      this.consumedCalories - this.intakeFat * 9 - this.intakeProtein * 4
    );
  }
}
</script>

<style scoped lang="scss">
.calc {
  background-color: #fafafa;
  border: 1px solid #eee;
}
</style>
