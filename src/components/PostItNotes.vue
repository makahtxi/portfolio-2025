<template>
  <div class="flex flex-col md:flex-row justify-between gap-5 my-8">
    <slot />
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
/* Each post-it note should be 30% width on desktop */
:deep(> *) {
  width: 100%;
}

@media (min-width: 768px) {
  :deep(> *) {
    width: 30%;
  }
}
</style>
