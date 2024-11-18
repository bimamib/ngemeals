<template>
  <div
    class="grid grid-cols-1 gap-5 px-8 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 2xl:grid-cols-5"
  >
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
  <div v-if="!meals.length" class="flex justify-center p-8 text-slate-600">
    There are no meals
  </div>
</template>

<script setup>
import MealItem from "./MealItem.vue";

const { meals } = defineProps({
  meals: {
    required: true,
    type: Array,
    default: () => [],
  },
});
</script>
