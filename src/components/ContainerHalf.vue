<template>
  <div class="flex flex-col md:flex-row justify-between my-20 gap-8 container-half">
    <slot />
  </div>
</template>

<script setup lang="ts">
</script>

<style scoped>
/* Child elements should be 45% width on desktop */
:deep(> *) {
  width: 100%;
}

@media (min-width: 768px) {
  :deep(> *) {
    width: 45%;
  }
}
</style>
