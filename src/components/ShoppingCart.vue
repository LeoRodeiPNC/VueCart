<template id="shopping-cart-template">
  <div>
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="(item, index) in cart" :key="index">
        {{ item.name }} - ${{ item.price }} ({{ item.quantity }})
        <button @click="increaseQuantity(index)">+</button>
        <button @click="decreaseQuantity(index)">-</button>
        <button @click="removeFromCart(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */
Vue.component("shopping-cart", {
  template: "#shopping-cart-template",
  props: ["cart"],
  methods: {
    removeFromCart(index) {
      this.$emit("remove-from-cart", index);
    },
    increaseQuantity(index) {
      this.$emit("increase-quantity", index);
    },
    decreaseQuantity(index) {
      this.$emit("decrease-quantity", index);
    },
  },
});
</script>
