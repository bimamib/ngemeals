<template>
  <Loading :visible="loading" />
  <div class="flex flex-col p-8 pb-0 text-red-600">
    <h1 class="mb-4 text-4xl font-bold">Random Meals</h1>
  </div>
  <Meals :meals="meals || []" />
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import store from "../store";
import axiosClient from "../axiosClient";
import Meals from "../components/Meals.vue";
import Loading from "../components/Loading.vue";

const meals = ref([]);
const loading = ref(true);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    await axiosClient.get(`random.php`).then(({ data }) => {
      meals.value.push(data.meals[0]);
    });
  }
  loading.value = false;
});
</script>
