<template>
  <div id="app">
    <orders-list></orders-list>
  </div>
</template>

<script>
import OrdersList from './components/orders/List.vue'

export default {
  name: 'App',
  components: {
    OrdersList
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
