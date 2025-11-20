<template>
  <div class="flex flex-col md:flex-row gap-8 max-w-[1200px] p-0 mb-12 box-border">
    <slot />
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
:deep(img) {
  @apply max-w-full;
}
</style>
