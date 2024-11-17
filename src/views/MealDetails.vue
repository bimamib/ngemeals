<template>
  <div class="w-[800px] mx-auto p-8">
    <pre>{{ meal }}</pre>
    <h1 class="mb-5 text-4xl font-bold">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" />
    <div
      class="grid grid-cols-1 py-2 text-lg sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-3"
    >
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div><strong class="font-bold">Area:</strong> {{ meal.strArea }}</div>
      <div><strong class="font-bold">Tags:</strong> {{ meal.strTags }}</div>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="mb-2 text-2xl font-semibold">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="mb-2 text-2xl font-semibold">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";

const route = useRoute();
const meal = ref({});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
  });
});
</script>
