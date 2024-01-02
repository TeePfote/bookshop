<!-- Login.vue -->
<template>
  <div>
    <h2>Admin Login</h2>
    <form id="form-container" @submit.prevent="login">
      <div class="mb-3">
        <label for="username" class="form-label">Username:</label>
        <input type="text" v-model="username" class="form-control" id="username" required />
      </div>
      <div class="mb-3">
        <label for="password" class="form-label">Password:</label>
        <input type="password" v-model="password" class="form-control" id="password" required />
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    login() {
      // Check if the provided username and password are correct
      if (this.username === "admin" && this.password === "adm24") {
        // Successful login
        this.$emit("login-success"); // Emit an event to notify the parent component
      } else {
        // Failed login
        console.log("Invalid username or password. Please try again.");
      }
    },
  },
};
</script>

<style>
/* Add any custom styles for the login form if needed */
</style>
