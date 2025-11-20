<template>
  <div class="w-full md:w-[40%]">
    <p class="text-xl font-semibold mb-2.5">{{ label }}</p>
    <p class="text-justify"><slot /></p>
  </div>
</template>

<script setup lang="ts">
interface Props {
  label: string;
}

defineProps<Props>();
</script>
