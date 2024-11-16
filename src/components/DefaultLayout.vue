<template>
  <div class="h-full bg-gray-100">
    <navbar />
    <main>
      <router-view />
    </main>
  </div>
</template>

<script setup>
import Navbar from "../components/Navbar.vue";
</script>
