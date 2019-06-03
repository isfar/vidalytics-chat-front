<template>
  <div id="app" class="container">
    <Chatbox />
  </div>
</template>

<script>
import Chatbox from './components/Chatbox.vue'
import Vue from "vue";
import VueResource from 'vue-resource';

Vue.use(VueResource);

export default {
  name: 'app',
  components: {
    Chatbox
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