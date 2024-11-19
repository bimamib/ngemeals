<template>
  <div class="p-8 pb-0">
    <h1 class="mb-4 text-4xl font-bold text-red-600">Ingredients</h1>
  </div>
  <div class="px-8">
    <div class="relative">
      <div
        class="absolute inset-y-0 start-0 flex items-center pointer-events-none z-20 ps-3.5"
      >
        <svg
          class="text-gray-400 shrink-0 size-4"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <circle cx="11" cy="11" r="8"></circle>
          <path d="m21 21-4.3-4.3"></path>
        </svg>
      </div>
      <input
        class="block w-full py-3 mb-3 text-sm border-gray-200 rounded-lg ps-10 pe-4 focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none"
        type="text"
        v-model="keyword"
        placeholder="Search for Ingredients..."
      />
    </div>
    <div
      class="grid grid-cols-1 gap-3 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 2xl:grid-cols-5"
    >
      <a
        href="#"
        @click.prevent="openIngredient(ingredient)"
        v-for="ingredient of computedIngredients"
        :key="ingredient.idIngredient"
        class="block px-3 py-3 mb-3 bg-white shadow rounded-xl"
      >
        <h3 class="mb-3 text-2xl font-bold">
          {{ ingredient.strIngredient }}
        </h3>
      </a>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";
import { useRouter } from "vue-router";
import store from "../store";

const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

function openIngredient(ingredient) {
  store.commit("setIngredient", ingredient);
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>
