<template>
  <div id="app">
    <div class="bg"></div>
    <div class="main">
      <Home msg="Welcome to Your Vue.js App" />
    </div>
  </div>
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
:root {
  --black: rgba(30, 30, 30, 1);
  --secondary-black: rgba(63, 63, 63, 1);
  --gray: rgba(220, 220, 220, 1);
  --light-blue: rgba(214, 230, 255, 1);
  --light-purple : rgba(253, 226, 255, 1);
  --blue : rgba(0, 39, 114, 1);
  --purple : rgba(114, 0, 96, 1);
}

body {
  margin: 0;
}

.main {
  position: relative;
  z-index: 10;
}

.bg {
  position: absolute;
  min-height: 50vh;
  width: 100%;
  z-index: 0;
  top: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--black);
  display: flex;
  min-height: 100vh;
  height: 100%;
  justify-content: center;
  align-items: center;
  background: #f0f0f0;
  position: relative;
}
</style>
