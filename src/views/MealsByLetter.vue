<template>
  <div class="p-8 pb-0">
    <h1 class="mb-4 text-4xl font-bold text-red-600">Meals by Letter</h1>
  </div>
  <div class="flex flex-wrap justify-center gap-3 px-8 mb-6">
    <router-link
      :to="{ name: 'byLetter', params: { letter } }"
      v-for="letter of letters"
      :key="letter"
      class="flex items-center justify-center w-2 h-2 transition-all hover:text-red-600 hover:scale-150"
      @click.native="startLoading"
    >
      {{ letter }}
    </router-link>
  </div>

  <!-- Loading Screen -->
  <Loading :visible="loading" />

  <!-- Meals List -->
  <Meals v-if="!loading" :meals="meals || []" />
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
import Meals from "../components/Meals.vue";
import Loading from "../components/Loading.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);
const loading = ref(false);

// Fungsi memulai loading sebelum rute berubah
function startLoading() {
  loading.value = true;
}

// Fungsi untuk memuat meals berdasarkan letter
async function fetchMealsByLetter(letter) {
  console.log("Loading starts for letter:", letter); // Debug
  loading.value = true;

  // Simulasi delay sebelum mengambil data (opsional)
  await new Promise((resolve) => setTimeout(resolve, 500)); // Simulasi delay

  // Memuat data berdasarkan huruf
  await store.dispatch("searchMealsByLetter", letter);

  // Simulasi delay setelah data selesai dimuat (opsional)
  await new Promise((resolve) => setTimeout(resolve, 500)); // Simulasi delay

  loading.value = false;
  console.log("Loading ends for letter:", letter); // Debug
}

// Observasi perubahan rute
// Observasi perubahan parameter letter di rute
watch(
  () => route.params.letter, // Parameter letter pada rute
  (newLetter) => {
    fetchMealsByLetter(newLetter); // Panggil fetch ketika letter berubah
  }
);

// Muat data untuk rute awal
onMounted(() => {
  fetchMealsByLetter(route.params.letter);
});
</script>
