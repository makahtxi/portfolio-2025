<template>
  <span :class="['font-semibold', colorClass]">
    <slot />
  </span>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  color?: 'purple' | 'teal' | 'orange' | 'dark';
}

const props = withDefaults(defineProps<Props>(), {
  color: 'purple'
});

const colorClass = computed(() => {
  const colors = {
    purple: 'text-orbit-purple',
    teal: 'text-orbit-teal',
    orange: 'text-orbit-orange',
    dark: 'text-orbit-dark'
  };
  return colors[props.color];
});
</script>
