<template>
  <div id="app">
    <Header msg="Welcome to Your Vue.js App"/>
    <Forms />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Forms from './components/Forms.vue'

export default {
  name: 'App',
  components: {
    Header,
    Forms
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
  height: 100%;
  width: 100%;
}
</style>
