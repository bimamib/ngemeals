<template>
  <!-- Detail Meals -->
  <Loading :visible="loading" />
  <div v-if="!loading" class="max-w-[800px] mx-auto p-10">
    <h1 class="mb-5 text-4xl font-bold">{{ meal.strMeal }}</h1>
    <div class="px-4 py-4 bg-white shadow rounded-xl">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="max-w-[100%] rounded-lg"
      />
    </div>
    <div class="flex flex-wrap gap-4 px-2 py-2 text-lg">
      <div class="flex flex-wrap items-center gap-1">
        <strong class="font-bold">Category:</strong>
        <span class="px-2 py-1 text-sm font-normal rounded-lg bg-slate-200">
          {{ meal.strCategory }}
        </span>
      </div>
      <div class="flex flex-wrap items-center gap-1">
        <strong class="font-bold">Area:</strong>
        <span class="px-2 py-1 text-sm font-normal rounded-lg bg-slate-200">
          {{ meal.strArea }}
        </span>
      </div>
      <div class="flex flex-wrap items-center gap-1">
        <strong class="font-bold">Tags:</strong>
        <span
          v-for="tag in getTags"
          :key="tag"
          class="px-2 py-1 text-sm font-normal rounded-lg bg-slate-200"
        >
          {{ tag }}
        </span>
        <span
          v-if="!getTags.length"
          class="px-2 py-1 text-sm font-normal rounded-lg bg-slate-200"
          >No tags available</span
        >
      </div>
    </div>

    <div class="my-3 text-base font-normal text-justify">
      {{ meal.strInstructions }}
    </div>

    <!-- Ingredients and Measures -->
    <div class="grid grid-cols-1 sm:grid-cols-2">
      <!-- Ingredients -->
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
      <!-- Measures -->
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

      <div class="mt-4">
        <YouTubeButton :href="meal.strYoutube" />
        <a
          :href="meal.strSource"
          target="_blank"
          class="inline-flex items-center px-3 py-2 ml-3 text-sm font-medium text-yellow-500 transition-colors hover:text-yellow-800 disabled:opacity-50 disabled:pointer-events-none"
        >
          View Original
        </a>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";
import { useRoute } from "vue-router";
import axiosClient from "../axiosClient";
import YouTubeButton from "../components/YouTubeButton.vue";
import Loading from "../components/Loading.vue";

const route = useRoute();
const meal = ref({});
const loading = ref(true);

const getTags = computed(() => {
  if (!meal.value.strTags) return [];
  // Filter untuk menghilangkan string kosong dan whitespace
  return meal.value.strTags
    .split(",")
    .map((tag) => tag.trim())
    .filter((tag) => tag.length > 0);
});

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`).then(({ data }) => {
    meal.value = data.meals[0] || {};
    loading.value = false;
  });
});
</script>
