<template>
  <div class="select" tabindex="1">
    <div v-for="option in options" :key="option.id">
      <input
        :value="option.option"
        v-model="category"
        class="selectopt"
        type="radio"
        :id="option.id"
      />
      <label :for="option.id" class="option">{{ option.text }}</label>
    </div>
  </div>
</template>

<script>
export default {
  name: "SelectNew",
  // props: {
  //   options: {
  //     type: Array,
  //     required: true,
  //   },
  // },
  emits: [],
  data() {
    return {
      options: [
        { option: "", id: "opt1", text: "Alla kategorier" },
        { option: "Fåglar", id: "opt2", text: "Fåglar" },
        { option: "Hundar", id: "opt3", text: "Hundar" },
        { option: "Katter", id: "opt4", text: "Katter" },
      ],
    };
  },
};
</script>
<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
}

.select {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 250px;
  height: 40px;
}

.option {
  padding: 0 30px 0 10px;
  min-height: 40px;
  display: flex;
  align-items: center;
  background: #333;
  border-top: #222 solid 1px;
  position: absolute;
  top: 0;
  width: 100%;
  pointer-events: none;
  order: 2;
  z-index: 1;
  transition: background 0.4s ease-in-out;
  box-sizing: border-box;
  overflow: hidden;
  white-space: nowrap;
  color: #fff;
}

.option:hover {
  background: #666;
}

.select:focus .option {
  position: relative;
  pointer-events: all;
}

input {
  opacity: 0;
  position: absolute;
  left: -99999px;
}

input:checked + label {
  order: 1;
  z-index: 2;
  background: #666;
  border-top: none;
  position: relative;
}

input:checked + label:after {
  content: "";
  width: 0;
  height: 0;
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-top: 5px solid white;
  position: absolute;
  right: 10px;
  top: calc(50% - 2.5px);
  pointer-events: none;
  z-index: 3;
}

input:checked + label:before {
  position: absolute;
  right: 0;
  height: 40px;
  width: 40px;
  content: "";
  background: #666;
}
.container {
  margin: 0 auto;
  width: 70%;
  display: flex;
  margin-top: 4.6rem;
  margin-bottom: 12rem;
}
.input-wrapper {
  display: flex;
  flex-direction: column;
  margin-left: 4rem;
}
.table {
  flex: 1;
}
.table__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2.6rem;
  color: $darker-blue;
  &__heading {
    font-size: 1.5rem;
    font-weight: bold;
  }
}
</style>
