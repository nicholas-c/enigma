<template>
  <div id="app">
    <h1>
      Enigma Machine
    </h1>

    <Enigma />
  </div>
</template>

<script>
import '@/assets/styles/main.css'
import Enigma from './components/Enigma'

export default {
  name: 'App',
  components: {
    Enigma
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
