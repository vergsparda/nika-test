<template>
  <PhotoApp msg="Тестoвое задание"/>
</template>

<script>
import PhotoApp from './components/PhotoApp.vue';

export default {
  name: 'App',
  components: {
    PhotoApp
    ,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #cadbed;
}

body {
  margin: 0;
  padding: 0;
}
</style>
