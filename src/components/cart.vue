<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-11 col-sm-8" id="cart">
        <button @click="showCart = !showCart" id="button">
          <span v-if="!showCart">Show Cart ({{ totalItems }})</span>
          <span v-else>Hide Cart</span>
        </button>
          <span class="ms-md-5" id="banner">the fakestore</span>
        <div v-if="showCart">
          <div class="mt-3 mb-2 ms-2">
            <div v-if="cart.length == 0" class="fw-bold">Your cart is empty</div>
            <div v-for="(item, index) in cart" :key="index">
              {{ item.quantity }} x {{ item.title }} - {{ item.price }}$
              <span id="remove" @click="remove(index)">[remove]</span>
            </div>
          </div>
          <div>Cart total items: {{ totalItems }} pcs</div>
          <div>Cart total amount: {{ totalPrice }}$</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["cart", "totalPrice", "totalItems"],
  data: () => {
    return {
      showCart: false,
    };
  },
  created: function () {
    window.addEventListener("scroll", this.handleScroll);
  },
  destroyed: function () {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll: function () {
      if (window.scrollY == 0) {
        this.showCart = false;
      }
    },
    remove(index) {
      this.$emit("remove", index);
    },
  },
};
</script>

<style>
#remove {
  margin-left: 10px;
  color: red;
  padding-inline: 3px;
  padding-bottom: 3px;
}
#remove:hover {
  background-color: lightgreen;
}
#cart {
  position: fixed;
  background-color: lightgray;
  border: grey solid;
  border-radius: 10px;
  padding: 10px;
  padding-top: 5px;
}
#banner {
  padding-left: 20%;
  font-size: 24px;
  position: relative;
  top: 2px;
}
#button {
  min-width: 130px;
}
</style>