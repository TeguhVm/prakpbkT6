<template>
  <div id="app">
    <name-list></name-list>
  </div>
</template>

<script>
import NameList from './components/NameList.vue';

export default {
  components: {
    NameList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}
body{
  background-image: url("src/teguh.jpg");
  background-repeat: no-repeat;
  background: cover;
  background-size: cover;
  margin: 0;
  place-items: center;
  min-width: auto;
  min-height: auto;
  margin-top: 300px;
}
</style>