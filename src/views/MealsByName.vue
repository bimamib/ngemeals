<template>
  <div class="p-8 pb-0">
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
        class="block w-full text-sm border-gray-200 rounded-lg ps-10 pe-4 focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none"
        type="text"
        v-model="keyword"
        placeholder="Search for Meals..."
        @change="searchMeals"
      />
    </div>
  </div>
  <div class="grid grid-cols-1 gap-5 p-8 md:grid-cols-3">
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
          <a
            :href="meal.strYoutube"
            target="_blank"
            class="inline-flex items-center px-3 py-2 text-sm font-medium text-red-800 transition-colors bg-red-100 border border-transparent rounded-lg gap-x-2 hover:bg-red-200 focus:outline-none focus:bg-red-200 disabled:opacity-50 disabled:pointer-events-none"
          >
            YouTube
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
