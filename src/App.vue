<template>
  <div id="app">
    <Layout/>
  </div>
</template>

<script>
// import home from './components/home.vue'
import Layout from './components/Layout.vue'
export default {
  name: 'app',
  components: {
    Layout
  }
}
</script>

<style>
body {
  margin:0;
}
#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
