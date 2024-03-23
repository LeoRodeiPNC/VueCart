<template>
  <div id="app">
    <h1>Vue Shopping Cart</h1>

    <!-- For ProductList Component -->
    <product-list :products="products" @add-to-cart="addToCart"></product-list>

    <!-- For ShoppingCart Component -->
    <shopping-cart
      :cart="cart"
      @remove-from-cart="removeFromCart"
      @increase-quantity="increaseQuantity"
      @decrease-quantity="decreaseQuantity"
    ></shopping-cart>

    <!-- For TotalPrice -->
    <p>Total Price: ${{ total }}</p>
  </div>
</template>

<script>
import ShoppingCart from "./components/ShoppingCart.vue";
import ProductList from "./components/ProductList.vue";

export default {
  components: {
    ShoppingCart,
    ProductList,
  },
  /* eslint-disable */
  new: vue({
    el: "#app",
    data: {
      products: [
        { id: 1, name: "Product One", price: 35 },
        { id: 2, name: "Product Two", price: 45 },
        { id: 3, name: "Product Three", price: 25 },
      ],
      cart: [],
    },
    computed: {
      total() {
        return this.cart.reduce(
          (acc, item) => acc + item.price * item.quantity,
          0
        );
      },
    },
    methods: {
      addToCart(product) {
        const found = this.cart.find((item) => item.id === product.id);
        if (found) {
          found.quantity++;
        } else {
          this.cart.push({
            id: product.id,
            name: product.name,
            price: product.price,
            quantity: 1,
          });
        }
      },
      removeFromCart(index) {
        this.cart.splice(index, 1);
      },
      increaseQuantity(index) {
        this.cart[index].quantity++;
      },
      decreaseQuantity(index) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity--;
        } else {
          this.removeFromCart(index);
        }
      },
    },
  }),
};
</script>

<style>
/* Global styles */
</style>
