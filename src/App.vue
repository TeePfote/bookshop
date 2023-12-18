<!-- App.vue -->
<template>
  <div id="app" class="text-center">
    <h1 class="h1">Bookshop Catalog</h1>
    <div class="card-container d-flex justify-content-center">
      <!-- First Row -->
      <book-card
          v-for="(title, index) in bookTitles"
          :key="index"
          :title="title"
          :description="bookDescriptions[index]"
          :image-src="imageSrc[index]"
      />
    </div>
  </div>
</template>

<script>
import BookCard from "@/components/BookCard.vue";

export default {
  name: "App",
  components: {
    BookCard,
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
        "/assets/book1.jpg",
        "/assets/book2.jpg",
        "/assets/book3.jpg",
        "/assets/book4.jpg",
        "/assets/book5.jpg",
        "/assets/book6.jpg",
        "/assets/book7.jpg",
      ]
    };
  },
  methods: {

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

.card-container {
  margin-top: 20px;
  flex-wrap: wrap;
  overflow-y: auto;
}

.h1 {
  margin-top: 20px;
}
</style>
