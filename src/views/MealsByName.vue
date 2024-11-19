<template>
  <div class="p-8 pb-0">
    <h1 class="mb-4 text-4xl font-bold text-red-600">Search Meals by Name</h1>
  </div>
  <div class="px-8 pb-3">
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
        placeholder="Search for Meals..."
        @change="searchMeals"
      />
    </div>
  </div>

  <Meals :meals="meals || []" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>
