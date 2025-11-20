<template>
  <img
    :src="src"
    :alt="alt"
    :class="[
      'w-full object-cover rounded-[var(--radius-card)]',
      aspectClasses
    ]"
  />
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  src: string;
  alt: string;
  aspect?: 'square' | 'video' | 'auto';
}

const props = withDefaults(defineProps<Props>(), {
  aspect: 'auto'
});

const aspectClasses = computed(() => {
  const aspects = {
    square: 'aspect-square',
    video: 'aspect-video',
    auto: ''
  };
  return aspects[props.aspect];
});
</script>
