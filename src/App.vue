<template>
  <div id="app">
    <!-- <Home /> -->
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>
<script>
// import Home from './views/Home.vue'

export default {
  name: "App", 
  components: {
    // Home
  },
}
</script>


<style lang="scss">
html,
body,#app{
  height: 100%;
}
</style>
