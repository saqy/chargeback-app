<template>
  <div id="app">
    <chargeback-container/>
  </div>
</template>

<script>
import ChargebackContainer from "./components/ChargebackContainer";
export default {
  name: "App",
  components: {
    // HelloWorld,
    ChargebackContainer,
  },
  methods: {
  }
};
</script>

<style>
@import "./assets/global.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
