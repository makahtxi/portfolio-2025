<template>
  <div
    :class="[
      'rounded-[10px] shadow-sm flex flex-col',
      noHeader ? 'pt-4 pb-6 px-4 items-center justify-start' : 'pt-2 px-4 pb-8',
      colorClasses
    ]"
  >
    <slot />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  color?: 'yellow' | 'purple' | 'teal' | 'orange' | 'light';
  noHeader?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  color: 'yellow',
  noHeader: false
});

const colorClasses = computed(() => {
  const colors = {
    yellow: 'bg-orbit-yellow text-orbit-dark',
    purple: 'bg-orbit-purple-light text-orbit-dark',
    teal: 'bg-orbit-teal text-white',
    orange: 'bg-orbit-orange text-orbit-dark',
    light: 'bg-white text-orbit-dark'
  };
  return colors[props.color];
});
</script>
