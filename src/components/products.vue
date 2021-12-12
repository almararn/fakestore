<template>
  <div>
    <div class="mt-2 mb-3">
      <input type="text" size="25" v-model="searchTerm" :placeholder="'Search in ' + categories"/>
    </div>
    <div v-if="spinner">
      <div class="d-flex justify-content-center mt-5">
        <div class="spinner-border text-secondary" role="status" style="width: 5rem; height: 5rem">
        </div>
      </div>
    </div>
    <div v-else>
      <div v-for="item in filteredItemsList" :key="item.id">
        <product :product="item" @addToCart="addToCart" />
      </div>
    </div>
  </div>
</template>

<script>
import product from "./products/product.vue";
export default {
  components: {
    product,
  },
  methods: {
    addToCart(item) {
      this.$emit("addToCart", item);
    },
  },
  props: ["productList", "categories", "search", "spinner"],
  data: () => {
    return {
      searchTerm: undefined,
    };
  },
  computed: {
    filteredItemsList() {
      if (!this.searchTerm) {
        return this.productList;
      } else {
        return this.productList.filter((product) => {
          return product.title
            .toLowerCase()
            .includes(this.searchTerm.toLowerCase());
        });
      }
    },
  },
};
</script>

<style>
</style>