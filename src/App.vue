<template>
  <div id="app">
    <note></note>
  </div>
</template>

<script>
import Note from './components/Note.vue'

export default {
  name: 'app',
  components: {
    Note
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
