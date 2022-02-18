<template>
  <div id="app">
    <img height="60px" src="./assets/unnamed.png">
    <groups></groups>
    <todo></todo>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import todo from './components/todo'
import groups from './components/groups.vue'
import Groups from './components/groups.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    groups,
    todo,
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
