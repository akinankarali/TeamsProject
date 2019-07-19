<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" @click="redirectFunc()" />
    <div class="container">
      <div class="row">
        <Cards @indexChanged="selectedCardIndex = $event"></Cards>
      </div>
    </div>
  </div>
</template>

<script>
import Cards from "./components/Cards.vue";

export default {
  name: "app",
  components: {
    Cards
  },
  props: ["selectedCardIndex"],
  methods: {
    redirectFunc() {
      window.location.href =
        "https://login.microsoftonline.com/d7b71368-8364-4c73-9b09-8ac643e76a61/oauth2/v2.0/authorize?client_id=f7b69c8e-ebb2-4da6-8f67-38813f8dd8c5&response_type=code&redirect_uri=http://localhost:8080&response_mode=query&scope=https%3A%2F%2Fgraph.microsoft.com%2Fgroup.read.all&state=11122";
    }
  }
};
</script>

<style>
</style>
