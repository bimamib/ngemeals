<template>
  <div
    v-if="visible"
    class="fixed inset-0 z-50 flex items-center justify-center bg-gray-900 bg-opacity-50 backdrop-blur-md"
  >
    <div
      class="w-16 h-16 border-t-4 border-b-4 border-white rounded-full animate-spin"
    ></div>
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
