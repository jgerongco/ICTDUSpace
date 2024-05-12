<script setup>
import Nav from "../components/Navbar.vue";
</script>

<template>
  <div class="home-container">
    <Nav/>
    <main>
      <h1>This is Homepage</h1>
    </main>
  </div>
</template>

<style scoped>
.home-container {
  background-image: url('src/NIY_03551.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  /* Additional styling if needed */
  min-height: 100vh; /* Ensure the background covers the entire viewport */
}
</style>
