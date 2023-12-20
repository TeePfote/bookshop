<!-- App.vue -->
<template>
  <div id="app" class="text-center">
    <div class="header-container">
      <h1 class="h1">Bookshop Catalog</h1>
      <!-- Search bar -->
      <div class="searchbar-container mt-3">
        <input type="text" v-model="searchQuery" class="form-control" placeholder="Search books..." />
      </div>
      <!-- Shopping Cart -->
      <div class="cart-container">
        <button class="btn btn-primary" @click="toggleShoppingCart">
          <svg xmlns="http://www.w3.org/2000/svg" height="16" width="18" viewBox="0 0 576 512" fill="#FFFFFF"><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2023 Fonticons, Inc.--><path d="M0 24C0 10.7 10.7 0 24 0H69.5c22 0 41.5 12.8 50.6 32h411c26.3 0 45.5 25 38.6 50.4l-41 152.3c-8.5 31.4-37 53.3-69.5 53.3H170.7l5.4 28.5c2.2 11.3 12.1 19.5 23.6 19.5H488c13.3 0 24 10.7 24 24s-10.7 24-24 24H199.7c-34.6 0-64.3-24.6-70.7-58.5L77.4 54.5c-.7-3.8-4-6.5-7.9-6.5H24C10.7 48 0 37.3 0 24zM128 464a48 48 0 1 1 96 0 48 48 0 1 1 -96 0zm336-48a48 48 0 1 1 0 96 48 48 0 1 1 0-96z"/></svg>
        </button>
        <shopping-cart
            :items="cartItems"
            v-if="showShoppingCart"
            @clear-cart="clearCart"/>
      </div>
    </div>
    <!-- Book cards -->
    <div class="card-container d-flex justify-content-center">
      <book-card
          v-for="(title, index) in filteredBookTitles"
          :key="index"
          :title="title"
          :description="bookDescriptions[index]"
          :image-src="imageSrc[index]"
          @add-to-cart="addToCart"
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
      bookTitles: [
        "To Kill a Mockingbird",
        "1984",
        "The Great Gatsby",
        "Harry Potter and the Sorcerer's Stone",
        "The Catcher in the Rye",
        "The Hobbit",
        "Coming soon",

      ],
      bookDescriptions: [
        "Classic novel by Harper Lee.",
        "Dystopian novel by George Orwell.",
        "F. Scott Fitzgerald's masterpiece.",
        "Fantasy novel by J.K. Rowling.",
        "J.D. Salinger's classic coming-of-age novel.",
        "Fantasy novel by J.R.R. Tolkien.",
        "Coming soon",

      ],
      imageSrc: [
        "/images/book1.jpg",
        "/images/book2.jpg",
        "/images/book3.jpg",
        "/images/book4.jpg",
        "/images/book5.jpg",
        "/images/book6.jpg",
        "/images/book7.jpg",
      ],
      showShoppingCart: false,
      cartItems: [],
      searchQuery: "", // New data property for search query
    };
  },
  computed: {
    // Computed property to filter book titles based on the search query
    filteredBookTitles() {
      return this.bookTitles.filter((title) =>
          title.toLowerCase().includes(this.searchQuery.toLowerCase())
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
  },
};
</script>

<style>
/* You can add custom styles here if needed */
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 20px;
}

.cart-container {
  margin-left: auto; /* Push the cart button to the right */
}

.card-container {
  margin-top: 10px;
  flex-wrap: wrap;
  overflow-y: auto;
}

.h1 {
  margin: 0;
}

.searchbar-container {
  margin-left: 6%;
}
</style>
