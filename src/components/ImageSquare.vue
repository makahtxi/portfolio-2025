<template>
  <img
    :src="src"
    :alt="alt"
    class="aspect-square w-full h-full object-cover rounded-2xl"
  />
</template>

<script setup lang="ts">
interface Props {
  src: string;
  alt: string;
}

defineProps<Props>();
</script>
