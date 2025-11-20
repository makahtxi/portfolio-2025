<template>
  <p>
    <span class="font-semibold text-orbit-purple">{{ label }}:</span>
    <slot />
  </p>
</template>

<script setup lang="ts">
interface Props {
  label: string;
}

defineProps<Props>();
</script>
