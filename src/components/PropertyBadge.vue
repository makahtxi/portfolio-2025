<template>
  <div>
    <p class="font-bold">{{ label }}</p>
    <p>{{ value }}</p>
  </div>
</template>

<script setup lang="ts">
interface Props {
  label: string;
  value: string;
}

defineProps<Props>();
</script>
