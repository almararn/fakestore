<template>
  <div class="pb-3">
    <div id="product">
      <div class="p-4">
        <div class="container">
          <div class="row align-items-center mb-3">
            <div class="col-4">
              <img :src="product.image" :alt="product.title" />
            </div>
            <div class="col-8">
              <button @click="addToCart(product)">Add to Cart</button>
            </div>
          </div>
        </div>
        <h4>{{ product.title }}</h4>
        <h3 id="price" class="fw-bold">{{ product.price }} $</h3>
        <p>{{ product.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"],
  methods: {
    addToCart(item) {
      this.$emit("addToCart", item);
    },
  },
};
</script>

<style scoped>
img {
  max-height: 100px;
}
#product {
  border: gray solid;
  border-radius: 10px;
  background-color: white;
}
#price {
  background-color: lightgray;
  padding-left: 15px;
  padding-top: 5px;
  padding-bottom: 5px;
  border-radius: 5px;
}
</style>