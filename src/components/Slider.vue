<template>
  <label>{{ text }}: {{ modelValue }} kr</label>
  <input
    :value="modelValue"
    type="range"
    step="10"
    min="0"
    max="1000"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<script>
export default {
  name: "Slider",
  props: {
    modelValue: {
      type: [Number, String],
      required: true,
    },
    text: {
      type: String,
      required: true,
    },
  },
  emits: ["update:modelValue"],
};
</script>
<style scoped lang="scss">
input[type="range"] {
  -webkit-appearance: none;
  margin: 18px 0;
  width: 100%;
}
input[type="range"]:focus {
  outline: none;
}
input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  background: #666;
}
input[type="range"]::-webkit-slider-thumb {
  height: 36px;
  width: 16px;
  background: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -14px;
}
input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #666;
}
label {
  margin-bottom: 0.4rem;
}
input {
  margin-bottom: 1rem;
}
</style>
