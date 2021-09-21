<template>
  <trafficLight msg="Test task for TrueConf company"/>
  <author />
</template>

<script>
import trafficLight from "./components/trafficLight.vue";
import author from "./components/author.vue";

export default {
  name: "App",
  components: {
    trafficLight,
    author,
  },
  methods: {
     mounted() {
      console.log(window.location.pathname)
     if (window.location.pathname === '/yellow') {
       console.log('Желтый!')
     }
    },
  }
};
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
