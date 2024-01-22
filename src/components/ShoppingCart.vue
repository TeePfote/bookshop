<!-- ShoppingCart.vue -->
<template>
  <div class="shopping-cart">
    <div>
      <h2>Shopping Cart</h2>
      <ul>
        <li v-for="(item, index) in groupedItems" :key="index">
          <button class="btn btn-sm btn-danger" @click="decrementCount(item)">
            <svg xmlns="http://www.w3.org/2000/svg" height="16" width="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M19 13H5v-2h14v2z" />
            </svg>
          </button>
          <span class="count">{{ item.count }}</span>
          <button class="btn btn-sm btn-success" @click="incrementCount(item)">
            <svg xmlns="http://www.w3.org/2000/svg" height="16" width="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M19 13H13v6h-2v-6H5v-2h6V5h2v6h6z" />
            </svg>
          </button>
          {{ item.title }}
        </li>
      </ul>
    </div>
    <div class="flex-row">
      <h3>Books: {{ bookCount }}</h3>
      <h3>Total: {{ totalPrice }}€</h3>
      <button class="btn btn-danger" @click="clearCart">Clear Cart</button>
      <button class="btn btn-primary" @click="redirectStripe">Checkout</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: Array,
  },
  computed: {
    // Computed property to group items and count occurrences
    groupedItems() {
      const grouped = [];
      const itemMap = new Map();

      // Count occurrences of each item
      this.items.forEach((item) => {
        const key = `${item.title}-${item.description}-${item.imageSrc}-${item.price}-${item.priceID}`;
        if (itemMap.has(key)) {
          itemMap.set(key, itemMap.get(key) + 1);
        } else {
          itemMap.set(key, 1);
        }
      });

      // Create an array of grouped items with counts
      itemMap.forEach((count, key) => {
        const [title, description, imageSrc, price, priceID] = key.split('-');
        grouped.push({
          title,
          description,
          imageSrc,
          price,
          priceID,
          count,
        });
      });

      return grouped;
    },
    // Computed property to calculate the total price
    totalPrice() {
      const total = this.groupedItems.reduce(
          (total, item) => total + parseFloat(item.price) * item.count,
          0
      );
      return parseFloat(total.toFixed(2));
    },
    // Count books in the cart
    bookCount() {
      return this.items.length;
    },
  },
  methods: {
    clearCart() {
      this.$emit("clear-cart");
    },
    decrementCount(item) {
      this.$emit("decrement-count", item);
    },
    incrementCount(item) {
      this.$emit("increment-count", item);
    },
    redirectStripe() {
      this.$emit("redirect-stripe");
    },
  },
};
</script>

<style scoped>
.shopping-cart {
  border: 1px solid #ccc;
  border-radius: 15px;
  padding: 15px;
  z-index: 1;
  width: 20vw;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
}

.count {
  margin: 0 8px;
  /* Adjust the margin as needed */
  font-weight: bold;
  /* Optional: make the count bold */
}

.btn-danger,
.btn-success {
  margin: 0 4px;
  /* Adjust the margin as needed */
}
</style>
