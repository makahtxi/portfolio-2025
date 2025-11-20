<template>
  <div class="flex flex-col md:flex-row justify-between mt-8 gap-4">
    <slot />
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
/* Child elements should be 49% width on desktop */
:deep(> *) {
  width: 100%;
}

@media (min-width: 768px) {
  :deep(> *) {
    width: 49%;
  }
}
</style>
