<template>
  <div class="container">
    <div class="table">
      <div class="table__header">
        <h1 class="table__header__heading">Sök produkter</h1>
        <ClearFilterButton :clearFilter="clearFilter" />
      </div>
      <ProductList :filterProducts="filterProducts" :sort="sort" />
    </div>
    <div class="input-wrapper">
      <Slider v-model="maxRange" text="Max pris" />
      <Search v-model="name" />
      <p class="option-heading">Sök på kategori</p>
      <div class="select" tabindex="1">
        <div v-for="option in options" :key="option">
          <input
            :value="option.option"
            v-model="category"
            class="selectopt"
            type="radio"
            :id="option.id"
          />
          <label v-bind:for="option.id" class="option">{{ option.text }}</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import ProductList from "../components/ProductList.vue";
import ClearFilterButton from "../components/ClearFilterButton.vue";
import Search from "../components/Search.vue";
import Slider from "../components/Slider.vue";
export default defineComponent({
  components: {
    ProductList,
    ClearFilterButton,
    Search,
    Slider,
  },
  data() {
    return {
      category: "",
      options: [
        { option: "", id: "opt1", text: "Alla kategorier" },
        { option: "Fåglar", id: "opt2", text: "Fåglar" },
        { option: "Hundar", id: "opt3", text: "Hundar" },
        { option: "Katter", id: "opt4", text: "Katter" },
      ],
      name: "",
      minRange: "0",
      maxRange: "1000",
      currentSort: "name",
      currentSortDir: "asc",
      products: [
        { name: "Alfågel", price: 350, category: "Fåglar" },
        { name: "Afghanhund", price: 987, category: "Hundar" },
        { name: "Abessinier", price: 456, category: "Katter" },
        { name: "Bergfink", price: 159, category: "Fåglar" },
        { name: "Azawakh", price: 567, category: "Hundar" },
        { name: "Bofink", price: 124, category: "Fåglar" },
        { name: "Saluki", price: 550, category: "Hundar" },
        { name: "Kärrhök", price: 675, category: "Fåglar" },
        { name: "Borzoi", price: 789, category: "Hundar" },
        { name: "Curl", price: 876, category: "Katter" },
        { name: "Vinthund", price: 765, category: "Hundar" },
        { name: "Uggla", price: 334, category: "Fåglar" },
        { name: "Balines", price: 456, category: "Katter" },
        { name: "Bengal", price: 567, category: "Katter" },
        { name: "Ejder", price: 199, category: "Fåglar" },
        { name: "Cymric", price: 127, category: "Katter" },
        { name: "Bondkatt", price: 265, category: "Katter" },
        { name: "Chart polski", price: 711, category: "Hundar" },
        { name: "Beckasin", price: 345, category: "Fåglar" },
        { name: "Devon rex", price: 7684, category: "Katter" },
        { name: "Burma", price: 765, category: "Katter" },
        { name: "Burmilla", price: 499, category: "Katter" },
        { name: "Chartreux", price: 298, category: "Katter" },
        { name: "Grågås", price: 300, category: "Fåglar" },
        { name: "Greyhound", price: 499, category: "Hundar" },
        { name: "Cornish Rex", price: 500, category: "Katter" },
        { name: "Magyar agar", price: 600, category: "Hundar" },
        { name: "Gråhäger", price: 124, category: "Fåglar" },
        { name: "Morkulla", price: 431, category: "Fåglar" },
        { name: "Varghund", price: 523, category: "Hundar" },
        { name: "Galgo", price: 678, category: "Hundar" },
      ],
    };
  },
  computed: {
    filterProducts() {
      return this.filterProductsByRange(
        this.filterProductsByName(
          this.filterProductsByCategory(this.sortedProducts(this.products))
        )
      );
    },
  },
  methods: {
    sort(category) {
      if (category === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = category;
    },
    filterProductsByCategory(products) {
      return products.filter(
        (product) => !product.category.indexOf(this.category)
      );
    },
    filterProductsByName(products) {
      return products.filter(
        (product) =>
          !product.name.toUpperCase().indexOf(this.name.toUpperCase())
      );
    },
    sortedProducts() {
      return this.products.slice().sort((a, b) => {
        let modifier = 1;
        if (this.currentSortDir === "desc") modifier = -1;
        if (a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
        if (a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
        return 0;
      });
    },
    filterProductsByRange(products) {
      return products.filter((product) =>
        product.price > 0 &&
        product.price >= this.minRange &&
        product.price <= this.maxRange
          ? product
          : ""
      );
    },
    clearFilter() {
      (this.category = ""),
        (this.name = ""),
        (this.minRange = "0"),
        (this.maxRange = "1000"),
        (this.currentSort = "name"),
        (this.currentSortDir = "asc");
    },
  },
});
</script>

<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
}

.option-heading {
  margin-bottom: 0.3rem;
}

.select {
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
  cursor: pointer;
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
