<!-- App.vue -->
<template>
  <div id="app" class="text-center">
    <div class="main">
      <div class="header-container">
        <h1 class="h1">Bookshop Catalog</h1>
        <!-- Search bar -->
        <div class="searchbar-container">
          <input type="text" v-model="searchQuery" class="form-control" placeholder="Search books..." />
        </div>
        <button class="btn btn-primary" @click="toggleShoppingCart">
          <svg xmlns="http://www.w3.org/2000/svg" height="16" width="18" viewBox="0 0 576 512" fill="#FFFFFF"><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2023 Fonticons, Inc.--><path d="M0 24C0 10.7 10.7 0 24 0H69.5c22 0 41.5 12.8 50.6 32h411c26.3 0 45.5 25 38.6 50.4l-41 152.3c-8.5 31.4-37 53.3-69.5 53.3H170.7l5.4 28.5c2.2 11.3 12.1 19.5 23.6 19.5H488c13.3 0 24 10.7 24 24s-10.7 24-24 24H199.7c-34.6 0-64.3-24.6-70.7-58.5L77.4 54.5c-.7-3.8-4-6.5-7.9-6.5H24C10.7 48 0 37.3 0 24zM128 464a48 48 0 1 1 96 0 48 48 0 1 1 -96 0zm336-48a48 48 0 1 1 0 96 48 48 0 1 1 0-96z"/></svg>
        </button>
      </div>
      <!-- Book cards -->
      <div class="card-container d-flex justify-content-center">
        <book-card
            v-for="(title, index) in filteredBookTitles"
            :key="index"
            :title="title.title"
            :description="title.description"
            :image-src="title.imageSrc"
            :price="title.price"
            @add-to-cart="addToCart"
        />
      </div>
    </div>
    <!-- Shopping Cart -->
    <div class="cart-container">
      <shopping-cart
          :items="cartItems"
          v-if="showShoppingCart"
          @clear-cart="clearCart"
          @increment-count="incrementCount"
          @decrement-count="decrementCount"
      />
    </div>
  </div>
</template>

<script>
import BookCard from "@/components/BookCard.vue";
import ShoppingCart from "@/components/ShoppingCart.vue";

export default {
  name: "App",
  components: {
    BookCard,
    ShoppingCart,
  },
  data() {
    return {
      books: [
        { title: "To Kill a Mockingbird", description: "Classic novel by Harper Lee.", imageSrc: "/images/book1.jpg", price: "10.99" },
        { title: "1984", description: "Dystopian novel by George Orwell.", imageSrc: "/images/book2.jpg", price: "8.99" },
        { title: "The Great Gatsby", description: "F. Scott Fitzgerald's masterpiece.", imageSrc: "/images/book3.jpg", price: "9.99" },
        { title: "Harry Potter and the Sorcerer's Stone", description: "Fantasy novel by J.K. Rowling.", imageSrc: "/images/book4.jpg", price: "14.99" },
        { title: "The Catcher in the Rye", description: "J.D. Salinger's classic coming-of-age novel.", imageSrc: "/images/book5.jpg", price: "9.99" },
        { title: "The Hobbit", description: "Fantasy novel by J.R.R. Tolkien.", imageSrc: "/images/book6.jpg", price: "14.99" },
        { title: "Coming soon", description: "Coming soon", imageSrc: "/images/book7.jpg", price: "19.99" },
      ],
      showShoppingCart: false,
      cartItems: [],
      searchQuery: "", // New data property for search query
    };
  },
  computed: {
    // Computed property to filter books based on the search query
    filteredBookTitles() {
      return this.books.filter((book) =>
          book.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    toggleShoppingCart() {
      this.showShoppingCart = !this.showShoppingCart;
    },
    addToCart(book) {
      this.cartItems.push(book);
      // Add any additional logic here (e.g., update total, show confirmation)
      console.log(`${book.title} added to cart!`);
    },
    clearCart() {
      this.cartItems = [];
    },
    decrementCount(item) {
      // Find the first item that has the same title, description, and image source
      const index = this.cartItems.findIndex(
          (cartItem) =>
              cartItem.title === item.title &&
              cartItem.description === item.description &&
              cartItem.imageSrc === item.imageSrc
      );
      // Remove if item is not null
      if (index !== -1) {
        this.cartItems.splice(index, 1);
      }
    },
    incrementCount(item) {
      this.cartItems.push(item);
      console.log(`${item.title} added to cart!`);
    },
  },
};
</script>

<style>
/* You can add custom styles here if needed */
#app {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100%;
}

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
}

.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 20px;
}

.cart-container {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 20px 16px;
}

.card-container {
  margin-top: 10px;
  flex-wrap: wrap;
  overflow-y: auto;
  /* height: 100%; */
}

.h1 {
  margin: 0;
}

.searchbar-container {
}
</style>
