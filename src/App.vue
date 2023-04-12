<template>
  <div id="app">
    <TextArea />
  </div>
</template>

<script>
import TextArea from './components/TextArea.vue'

export default {
  name: 'App',
  components: {
    TextArea
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
