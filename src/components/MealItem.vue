<template>
  <div class="bg-white border shadow rounded-xl">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <div class="p-3">
        <img
          :src="meal.strMealThumb"
          :alt="strMeal"
          class="object-cover w-full h-48 rounded-lg"
        />
      </div>
    </router-link>
    <div class="p-3">
      <h2 class="font-bold">{{ meal.strMeal }}</h2>
      <p class="mb-4 text-justify">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime ex,
        sequi, ab dolore harum sapiente blanditiis ipsam debitis, voluptatum
        minima velit itaque officiis dolores doloremque. Voluptatibus sunt ex
        non aut!
      </p>
      <div class="flex items-center justify-between">
        <YouTubeButton :href="meal.strYoutube">YouTube</YouTubeButton>
      </div>
    </div>
  </div>

  <div
    v-for="meal of meals"
    :key="meal.idMeal"
    class="bg-white border shadow rounded-xl"
  >
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <div class="p-3">
        <img
          :src="meal.strMealThumb"
          :alt="strMeal"
          class="object-cover w-full h-48 rounded-lg"
        />
      </div>
    </router-link>
    <div class="p-3">
      <h2 class="font-bold">{{ meal.strMeal }}</h2>
      <p class="mb-4 text-justify">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime ex,
        sequi, ab dolore harum sapiente blanditiis ipsam debitis, voluptatum
        minima velit itaque officiis dolores doloremque. Voluptatibus sunt ex
        non aut!
      </p>
      <div class="flex items-center justify-between">
        <YouTubeButton :href="meal.strYoutube">YouTube</YouTubeButton>
      </div>
    </div>
  </div>
</template>

<script setup>
const { meal } = defineProps({
  meal: Object,
});
</script>
