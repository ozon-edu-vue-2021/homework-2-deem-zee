<template>
  <div id="app">
    <TreeStructure
      :node="node_modules"
    />
  </div>
</template>

<script>

import TreeStructure from './components/TreeStructure.vue';
import node_modules from '../public/static/node_modules.json';

export default {
  name: 'app',
  data() {
    return {
      node_modules,
    }
  },
  components: {
    TreeStructure
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}

</style>
