<!-- BookCard.vue -->
<template>
  <div class="card" style="width: 18rem; margin-right: 10px;">
    <img :src="imageSrc" class="card-img-top" alt="Book Cover Image" data-toggle="tooltip" :title="title">
    <div class="card-body">
      <h5 class="card-title">{{ title }}</h5>
      <p class="card-text">{{ description }}</p>
      <p class="card-text">{{ price }}$</p>
      <div class="d-flex justify-content-between align-items-center">
        <a href="#" class="btn btn-primary" @click="comingSoon">Read more</a>
        <button class="btn btn-success" @click="addToCart">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    description: String,
    imageSrc: String,
    price: Number,
    priceID: String,
    stockCount: Number,
  },
  methods: {
    addToCart() {
      // Emit the add-to-cart event with the book information
      this.$emit("add-to-cart", {
        title: this.title,
        description: this.description,
        imageSrc: this.imageSrc,
        price: this.price,
        priceID: this.priceID,
        stockCount: this.stockCount,
      });
    },
    comingSoon() {
      alert("Coming Soon!");
    },
  },
};
</script>

<style>
/* You can add custom styles here if needed */
.card {
  width: calc(33.33% - 10px);
  /* Adjust the width and margin between cards as needed */
  margin-right: 10px;
  margin-bottom: 20px;
  /* Add margin at the bottom for spacing between rows */
}

.card-body {
  display: flex;
  flex-direction: column;
}

.card-text {
  flex: 1;
  /* Make the description take up all the space it can */
}

.card:last-child {
  margin-right: 0;
  /* Remove margin for the last card in each row */
}

.card-img-top {
  height: 200px;
  /* Adjust the desired height */
  object-fit: cover;
  /* or "contain" based on your preference */
}
</style>
