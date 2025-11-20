<template>
  <div :class="gridClasses">
    <slot />
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  columns?: 1 | 2 | 3 | 4;
  gap?: 'sm' | 'md' | 'lg' | 'xs';
  variant?: 'default' | 'grid2x2';
}

const props = withDefaults(defineProps<Props>(), {
  columns: 2,
  gap: 'md',
  variant: 'default'
});

const gridClasses = computed(() => {
  if (props.variant === 'grid2x2') {
    return 'grid grid-cols-2 grid-rows-2 gap-[1%] max-w-[1200px] w-full';
  }

  const columnClasses = {
    1: 'grid-cols-1',
    2: 'grid-cols-1 md:grid-cols-2',
    3: 'grid-cols-1 md:grid-cols-3',
    4: 'grid-cols-2 md:grid-cols-4'
  };

  const gapClasses = {
    xs: 'gap-1',
    sm: 'gap-2',
    md: 'gap-5',
    lg: 'gap-8'
  };

  return ['grid', 'w-full', columnClasses[props.columns], gapClasses[props.gap]].join(' ');
});
</script>

<style scoped>
:deep(> *) {
  width: 100%;
}
</style>
