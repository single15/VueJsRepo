<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" height="150">
    <FilterArticles title="Filter LearnVue Articles" />
  </div>
</template>

<script>
import FilterArticles from './components/FilterArticles.vue';

export default {
  name: 'App',
  components: {
    FilterArticles
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
