<template>
  <HelloWorld msg="Track Your Tasks"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
  width: 70%;
  margin: auto;
  min-height: 500px;
}
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #fafafa;
}
</style>
