<template>
  <img
    :src="src"
    :alt="alt"
    :class="[
      'w-full object-contain',
      shadow && 'shadow-md',
      roundedClass,
      aspectClass
    ]"
  />
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  src: string;
  alt: string;
  rounded?: 'none' | 'small' | 'mini';
  shadow?: boolean;
  aspect?: 'auto' | 'square' | 'video';
}

const props = withDefaults(defineProps<Props>(), {
  rounded: 'none',
  shadow: false,
  aspect: 'auto'
});

const roundedClass = computed(() => {
  const classes = {
    none: '',
    small: 'rounded-[15px]',
    mini: 'rounded-[8px]'
  };
  return classes[props.rounded];
});

const aspectClass = computed(() => {
  const classes = {
    auto: '',
    square: 'aspect-square object-cover',
    video: 'aspect-video object-cover'
  };
  return classes[props.aspect];
});
</script>
