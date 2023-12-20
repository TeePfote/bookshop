<!-- ShoppingCart.vue -->
<template>
  <div class="shopping-cart">
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    items: Array,
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
  border-radius: 20px;
  padding: 10px;
  z-index: 1;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}
</style>
