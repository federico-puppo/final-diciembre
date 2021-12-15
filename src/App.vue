<template>
  <div id="app">
    <Conversor/>
    <p>Respuestas:</p>
    <p>1) C</p>
    <p>2) B</p>
    <p>3) C</p>
    <p>4) A</p>
    <p>5) B C</p>
  </div>
</template>

<script>
import Conversor from './components/Conversor.vue'

export default {
  name: 'App',
  components: {
    Conversor
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
</style>
