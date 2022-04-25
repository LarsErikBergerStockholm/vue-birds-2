<template>
  <button @click="clearFilter">Rensa filter</button>
</template>

<script>
export default {
  name: "ClearFilterButton",
  props: {
    clearFilter: {
      type: Function,
      required: true,
    },
  },
};
</script>
<style lang="scss">
button {
  display: inline-block;
  padding: 0.7em 1.7em;
  text-decoration: none;
  color: #ffffff;
  background-color: #666;
  text-align: center;
  position: relative;
}
</style>
