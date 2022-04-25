<template>
  <form className="search">
    <label className="search__label">Sök på djur</label>
    <input
      :value="modelValue"
      type="text"
      placeholder="Sök på djur"
      @input="updateInput"
    />
  </form>
</template>

<script>
export default {
  name: "Search",
  props: {
    modelValue: {
      type: String,
      required: true,
    },
  },
  emits: ["update:modelValue"],
  methods: {
    updateInput(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>
<style scoped lang="scss">
input {
  padding: 0.65rem;
  border-radius: 0rem;
  border-width: 0rem;
}
.search {
  display: flex;
  flex-direction: column;
  margin-bottom: 0.7rem;
  &__label {
    margin-bottom: 0.3rem;
  }
}
</style>
