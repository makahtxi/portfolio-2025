<template>
  <div :class="[
    'py-4 flex gap-5', 
    direction === 'column' ? 'flex-col items-start' : 'flex-row flex-wrap'
  ]">
    <slot />
  </div>
</template>

<script setup lang="ts">
interface Props {
  direction?: 'row' | 'column';
}

withDefaults(defineProps<Props>(), {
  direction: 'row'
});
</script>
