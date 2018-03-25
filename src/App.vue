<template>
  <div id="app">
    <directed-graph></directed-graph>
  </div>
</template>

<script>
import DirectedGraph from './components/DirectedGraph'
export default {
  name: 'app',
  components: {
    DirectedGraph
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}
</style>
