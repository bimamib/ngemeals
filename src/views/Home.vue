<template>
  <div class="flex flex-col p-8 pb-0 text-red-600">
    <h1 class="mb-4 text-4xl font-bold">Random Meals Meals</h1>
  </div>
  <Meals :meals="meals || []" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
});
</script>
