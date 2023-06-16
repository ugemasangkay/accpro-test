<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <NumberPickerGame/>
</template>

<script>
import NumberPickerGame from './components/NumberPickerGame.vue'

export default {
  name: 'App',
  components: {
    NumberPickerGame
  }
}
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

img {
  max-width: 100px;
}
</style>
