<template>
  <div id="categories">
      <input type="radio" class="form-check-input mx-1" id="all" value="all categories" v-model="categRadio" @click="selectCategory('all categories')">
      <label class="me-2" for="all categories">all categories</label>
      <span v-for="category in categories" :key="category">
      <input type="radio" class="me-1" :id="category" :value="category" v-model="categRadio" @click="selectCategory(category)">
      <label class="me-2" :for="category">{{ category }}</label>
      </span>
  </div>
</template>

<script>
export default {
  props: ["categories"],
  methods: {
    selectCategory(category) {
      this.$emit("setCategory", category);
      this.categRadio = undefined
    },
  },
  data: () => {
    return {
      categRadio: 'all categories'
    };
  },
};
</script>

<style>
#categories{
  padding-top: 80px;
}
</style>