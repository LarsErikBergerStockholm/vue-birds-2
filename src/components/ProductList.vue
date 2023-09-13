<template>
  <div class="wrapper">
    <div class="sort">
      <ul class="sort__items">
        <li class="sort__item" @click="sort('name')">Djur</li>
        <li class="sort__item" @click="sort('price')">Pris</li>
        <li class="sort__item" @click="sort('category')">Kategori</li>
      </ul>
    </div>
    <div class="list">
      <ul
        class="list__items"
        v-for="product in filterProducts"
        :key="product.id"
      >
        <li class="list__item">{{ product.name }}</li>
        <li class="list__item">{{ product.price }}</li>
        <li class="list__item">{{ product.category }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductList",
  props: {
    filterProducts: {
      type: Array,
      required: true,
    },
    sort: {
      type: Function,
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

<style lang="scss">
.wrapper {
  // width: 28rem;
}
.sort__items {
  display: flex;
  justify-content: space-between;
  padding: 2rem;
  cursor: pointer;
}
.sort__item {
  list-style: none;
  font-weight: bold;
}
.list__items {
  display: flex;
  justify-content: space-between;
  background-color: $white;
  padding: 2rem;
}
.list__item {
  list-style: none;
}
</style>
