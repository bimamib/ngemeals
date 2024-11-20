<template>
  <div
    v-if="visible"
    class="fixed inset-0 z-50 flex items-center justify-center bg-gray-900 bg-opacity-50 backdrop-blur-md"
  >
    <div class="flex flex-col items-center justify-center w-full gap-4">
      <div
        class="flex items-center justify-center text-4xl text-blue-500 border-4 border-transparent rounded-full w-14 h-14 animate-spin border-t-blue-500"
      >
        <div
          class="flex items-center justify-center w-10 h-10 text-2xl text-red-500 border-4 border-transparent rounded-full animate-spin border-t-red-500"
        ></div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  visible: {
    type: Boolean,
    default: false,
  },
});
</script>

<style scoped>
/* Optional: Customize the spinning animation if needed */
</style>
