<template>
  <PhotoApp msg="Тестoвое задание"/>
</template>

<script>
import PhotoApp from './components/PhotoApp.vue';

export default {
  name: 'App',
  components: {
    PhotoApp,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #cadbed;
  margin: 30px
}

body {
  margin: 0;
  padding: 0;
}
button {
  display: flex;
  width: 100%;
  cursor: pointer;
  border: none;
  background-color: unset;
  align-items: center;

  &:hover {
    background-color: #dae4ef;
  }
}
</style>
