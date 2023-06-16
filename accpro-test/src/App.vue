<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <TransactionSummary />
</template>

<script>
import TransactionSummary from "./components/TransactionSummary.vue";

export default {
  name: "App",
  components: {
    TransactionSummary,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
