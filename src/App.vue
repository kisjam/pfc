<template>
  <div id="app">
    <Calcs />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Calcs from "./components/Calcs.vue";

@Component({
  components: {
    Calcs
  }
})
export default class App extends Vue {}
</script>
