<template id="product-list-template">
  <div>
    <h2>Products</h2>
    <ul>
      <li v-for="product in products" :key="product.id">
        {{ product.name }} - ${{ product.price }}
        <button @click="addToCart(product)">Add to Cart</button>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */
Vue.component("product-list", {
  template: "#product-list-template",
  props: ["products"],
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
  },
});
</script>
