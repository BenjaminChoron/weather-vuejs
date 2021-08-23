<template>
  <div id="app">
    <Weather></Weather>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'

export default {
  name: 'App',
  components: {
    Weather
  }
}
</script>

<style>
body {
  display: flex;
  justify-content: center;
  min-height: 100vh;
  background-image: url('./assets/blurry-gradient-haikei.svg');
  background-size: cover;
}
</style>
