<template>
  <div id="app">
    <List 
      :items="items"
    />
  </div>
</template>

<script>
import List from './components/List.vue';
import items from '../public/static/node_modules.json';

export default {
  name: 'App',

  data() {
    return {
      items
    }
  },

  components: {
    List
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
