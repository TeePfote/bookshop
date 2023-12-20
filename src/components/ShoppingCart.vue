<!-- ShoppingCart.vue -->
<template>
  <div class="shopping-cart">
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item.title }}</li>
    </ul>
    <button class="btn btn-danger" @click="clearCart">Clear Cart</button>
  </div>
</template>

<script>
export default {
  props: {
    items: Array,
  },
  methods: {
    clearCart() {
      this.$emit("clear-cart");
    },
  },
};
</script>

<style scoped>
/* Add styles for the shopping cart */
.shopping-cart {
  position: absolute;
  top: 5%; /* Adjust the distance from the top */
  right: 2%; /* Adjust the distance from the right */
  border: 1px solid #ccc;
  border-radius: 15px;
  padding: 15px;
  z-index: 1;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

.btn-danger {
  margin-top: 10px; /* Adjust the margin as needed */
}
</style>
