<template>
  <div class="transition-all bg-white border shadow rounded-xl hover:scale-105">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <div class="p-3">
        <img
          :src="meal.strMealThumb"
          :alt="meal.strMeal"
          class="object-cover w-full h-48 rounded-lg"
        />
      </div>
    </router-link>
    <div class="p-3">
      <h2 class="font-bold">{{ meal.strMeal }}</h2>
      <p class="mb-4 text-justify">
        {{ $filters.truncateWords(meal.strInstructions, 20) }}
      </p>
      <div class="flex items-center justify-between">
        <YouTubeButton :href="meal.strYoutube" />
      </div>
    </div>
  </div>
</template>

<script setup>
import YouTubeButton from "./YouTubeButton.vue";

const { meal } = defineProps({
  meal: {
    required: true,
    type: Object,
    default: () => ({}),
  },
});
</script>
