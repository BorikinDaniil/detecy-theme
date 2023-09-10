<template>
  <div id="app">
    <div id="detection"
         style="display: none; background-color: canvas; color-scheme: light">
    </div>
    <h1>
      isDarkFromOS - {{ isDarkFromOS }}
    </h1>
    <h1>
      isForcedDarkChrome - {{ isForcedDarkChrome }}
    </h1>
    <h1>
      isChrome - {{ isChrome }}
    </h1>
    <h1>
      newColorScheme - {{ newColorScheme }}
    </h1>
  </div>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    isDarkFromOS: '',
    isForcedDarkChrome: '',
    isChrome: '',
    newColorScheme: '',
  }),

  mounted() {
    if (window.matchMedia) {
      console.log('window.matchMedia', window.matchMedia)
      const isDarkFromOS = window.matchMedia('(prefers-color-scheme: dark)').matches;
      this.isDarkFromOS = isDarkFromOS
      console.log('isDarkFromOS', isDarkFromOS)
      console.log('window.matchMedia(prefers-color-scheme: dark', window.matchMedia('(prefers-color-scheme: dark)'))

      const detectionDiv = document.querySelector('#detection');
      // If the computed style is not white then the page is in Auto Dark Theme.
      const isForcedDarkChrome = getComputedStyle(detectionDiv).backgroundColor != 'rgb(255, 255, 255)';
      console.log('isForcedDarkChrome', isForcedDarkChrome)
      this.isForcedDarkChrome = isForcedDarkChrome

      const isChrome = navigator.userAgent.indexOf("Chrome") != -1;
      console.log('isChrome', isChrome)
      this.isChrome = isChrome

      window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
        const newColorScheme = event.matches ? "dark" : "light";
        console.log('newColorScheme', newColorScheme)
        this.newColorScheme = newColorScheme
      });
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
