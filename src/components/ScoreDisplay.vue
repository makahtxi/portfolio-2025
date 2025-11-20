<template>
  <div
    class="flex flex-col justify-between items-center w-48/100 lg:w-24/100 h-30 lg:h-35 mb-8 text-white"
  >
    <p class="text-lg lg:text-base text-center font-medium">
      {{ label }}
    </p>
    <p class="font-extrabold">
      <span class="text-6xl">{{ score }}</span>
      <span class="text-3xl">{{ suffix }}</span>
    </p>
  </div>
</template>

<script setup lang="ts">
interface Props {
  label: string;
  score: string | number;
  suffix: string;
}

defineProps<Props>();
</script>
