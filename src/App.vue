<template>
  <Filter />
</template>

<script>
import Filter from "./components/Filter.vue";

export default {
  name: "App",
  components: {
    Filter,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: $black;
  display: flex;
  justify-content: center;
  background-image: linear-gradient(to top, $light-blue, $white);
}
</style>
