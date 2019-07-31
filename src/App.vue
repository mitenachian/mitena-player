<template>
  <div id="app">
    <musicTopBox/>
    <musicList/>
  </div>
</template>

<script>
import musicTopBox from './components/musicTopBox.vue'
import musicList from './components/musicList.vue'
export default {
  name: 'app',
  components: {
    musicTopBox,
    musicList
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}
</style>
