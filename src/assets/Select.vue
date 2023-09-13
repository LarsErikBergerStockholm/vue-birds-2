<template>
  <label>Sök </label>
  <select
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  >
    <option value="">--Välj kategori--</option>
    <option v-for="option in options" :value="option" :key="option">
      {{ option }}
    </option>
  </select>
</template>

<script>
export default {
  name: "Select",
  props: {
    modelValue: {
      type: String,
      required: true,
    },
  },
  emits: ["update:modelValue"],
  data() {
    return {
      options: ["Fåglar", "Hundar", "Katter"],
    };
  },
};
</script>
<style scoped lang="scss">
label {
  margin-bottom: 0.3rem;
}
</style>
