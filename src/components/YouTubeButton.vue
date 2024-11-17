<template>
  <a
    :href="href"
    target="_blank"
    class="inline-flex items-center px-3 py-2 text-sm font-medium text-red-800 transition-colors bg-red-100 border border-transparent rounded-lg gap-x-2 hover:bg-red-200 focus:outline-none focus:bg-red-200 disabled:opacity-50 disabled:pointer-events-none"
  >
    <slot></slot>
  </a>
</template>

<script setup>
const props = defineProps({
  href: String,
});
</script>
