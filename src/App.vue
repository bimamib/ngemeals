<template>
  <div class="h-full bg-gray-100">
    <header
      class="flex items-stretch justify-between h-16 bg-white border shadow"
    >
      <router-link
        :to="{ name: 'home' }"
        class="inline-flex items-center h-full px-5"
      >
        Home
      </router-link>
      <div class="flex items-center gap-2">
        <router-link
          :to="{ name: 'byName' }"
          class="inline-flex items-center h-full px-2 transition-colors hover:bg-teal-100"
        >
          Search Meals
        </router-link>
        <router-link
          :to="{ name: 'byLetter' }"
          class="inline-flex items-center h-full px-2 transition-colors hover:bg-teal-100"
        >
          Meals By Letter
        </router-link>
        <router-link
          :to="{ name: 'byIngredient' }"
          class="inline-flex items-center h-full px-2 transition-colors hover:bg-teal-100"
        >
          Meals By Ingredients
        </router-link>
      </div>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<script setup></script>

<style scoped></style>
