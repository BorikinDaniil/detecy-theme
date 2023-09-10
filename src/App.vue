<template>
  <div id="app">
    <div id="detection"
         style="display: none; background-color: canvas; color-scheme: light">
    </div>
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },

  mounted() {
    if (window.matchMedia) {
      console.log('window.matchMedia', window.matchMedia)
      const isDarkFromOS = window.matchMedia('prefers-color-scheme: dark').matches;
      console.log('isDarkFromOS', isDarkFromOS)

      const detectionDiv = document.querySelector('#detection');
      // If the computed style is not white then the page is in Auto Dark Theme.
      const isForcedDarkChrome = getComputedStyle(detectionDiv).backgroundColor != 'rgb(255, 255, 255)';
      console.log('isForcedDarkChrome', isForcedDarkChrome)

      const isChrome = navigator.userAgent.indexOf("Chrome") != -1;
      console.log('isChrome', isChrome)
    }
  },
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
</style>
