<template>
  <div class="container mt-3">
    <cart
      :cart="cart"
      :totalPrice="totalPrice"
      :totalItems="totalItems"
      @remove="remove"/>
    <categories :categories="cate" @setCategory="setCategory" />
    <products
      :categories="selectedCategory"
      :productList="filteredProducts"
      :spinner="spinner"
      @addToCart="buyProduct"/>
  </div>
</template>

<script>
import axios from "axios";
import categories from "./components/categories.vue";
import products from "./components/products.vue";
import cart from "./components/cart.vue";

export default {
  name: "App",
  components: {
    categories,
    products,
    cart,
  },
  data: () => {
    return {
      cate: [],
      products: [],
      cart: [],
      selectedCategory: "all categories",
      totalItems: 0,
      totalPrice: 0,
      firstPrice: 0,
      spinner: false,
    };
  },
  computed: {
    filteredProducts() {
      if (this.selectedCategory != "all categories") {
        return this.products.filter((item) => {
          return item.category === this.selectedCategory;
        });
      } else {
        return this.products;
      }
    },
  },
  methods: {
    buyProduct(product) {
      let tempItem = undefined;
      this.cart.forEach((i) => {
        if (product.title === i.title) {
          tempItem = i;
        }
      });

      if (tempItem != undefined) {
        tempItem.quantity++;
      } else {
        this.cart.push({
          title: product.title,
          price: product.price,
          quantity: 1,
        });
      }

      this.totalItems++;
      this.firstPrice += product.price;
      this.totalPrice = this.firstPrice.toFixed(2);
    },
    remove(index) {
      this.totalItems =
        parseInt(this.totalItems) - parseInt(this.cart[index].quantity);
      this.firstPrice =
        parseFloat(this.totalPrice) -
        parseFloat(this.cart[index].price) *
          parseInt(this.cart[index].quantity);
      this.totalPrice = this.firstPrice.toFixed(2);
      this.cart.splice(index, 1);
    },
    setCategory(cate) {
      this.selectedCategory = cate;
    },
  },
  mounted() {
    this.spinner = true;
    axios
      .get("https://fakestoreapi.com/products")
      .then((resp) => {
        this.spinner = false;
        this.products = resp.data;
      })
      .catch((error) => console.log(error));
      
     axios
      .get("https://fakestoreapi.com/products/categories")
      .then((res) => {
        this.cate = res.data;
      })
      .catch((error) => console.log(error)); 
  },
};
</script>

<style>
body {
  background-color: wheat;
}
</style>
