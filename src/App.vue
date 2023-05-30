<template>
  <trisGenerate :title="titleT"></trisGenerate>
</template>

<script>
import trisGenerate from "./components/tris.vue";

export default {
  name: "App",
  components: {
    trisGenerate,
  },
  data() {
    return {
      titleT: "",
    };
  },
  mounted() {
    this.titleT = "Tic tac toe Game with Vue.js";
  },
};
</script>
<style>
#app {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
