<template>
  <button
    v-if="!closable"
    :class="[
      'py-[0.51em] px-8 rounded-full font-medium font-sans transition-all duration-200 ease-in-out',
      'hover:cursor-pointer hover:opacity-90 hover:scale-[0.98]',
      variantClasses
    ]"
  >
    <slot />
  </button>

  <button
    v-else
    :class="[
      'flex items-center font-sans p-0 rounded-full transition-all duration-200 ease-in-out',
      variantClasses
    ]"
  >
    <span class="pr-2 pl-4 font-medium">
      <slot />
    </span>
    <div class="bg-white/10 w-[1px] h-[75%]"></div>
    <div class="h-full flex items-center pr-4 pl-2 py-[0.8em] hover:bg-black/10 hover:cursor-pointer transition-all duration-200 rounded-r-full">
      <svg width="12" height="12" viewBox="0 0 6 6" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M4.94012 1.01419L1.15283 4.80148" stroke="currentColor" stroke-width="0.908948" stroke-linecap="round"/>
        <path d="M4.93982 4.80148L1.15253 1.01419" stroke="currentColor" stroke-width="0.908948" stroke-linecap="round"/>
      </svg>
    </div>
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  variant?: 'purple' | 'teal' | 'orange' | 'dark' | 'blue' | 'yellow';
  closable?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'purple',
  closable: false
});

const variantClasses = computed(() => {
  const variants = {
    purple: 'bg-orbit-purple-light text-orbit-light',
    teal: 'bg-orbit-teal text-orbit-light',
    orange: 'bg-orbit-orange text-orbit-dark',
    dark: 'bg-orbit-dark text-orbit-light',
    blue: 'bg-orbit-blue text-orbit-light',
    yellow: 'bg-orbit-yellow text-orbit-dark'
  };
  return variants[props.variant];
});
</script>
