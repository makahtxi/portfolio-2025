<template>
  <nav class="fixed top-0 left-0 right-0 z-50 bg-[#1e1e1e]/80 backdrop-blur-md border-b border-[#676767] w-full px-8 md:px-[253px] py-4">
    <div class="flex items-center justify-between w-full">
      <!-- Logo -->
      <a href="/">
        <img src="/logo.svg" alt="Logo" class="w-8 h-11" />
      </a>

      <!-- Navigation Links -->
      <div class="flex gap-8 items-center text-white text-base">
        <a
          href="/projects"
          :class="['relative hover:opacity-80 transition-opacity', isProjectsActive && 'active-link']"
        >
          Projects
          <span v-if="isProjectsActive" class="absolute left-0 right-0 -bottom-1 h-px bg-white"></span>
        </a>
        <a
          href="/about"
          :class="['relative hover:opacity-80 transition-opacity', isAboutActive && 'active-link']"
        >
          About
          <span v-if="isAboutActive" class="absolute left-0 right-0 -bottom-1 h-px bg-white"></span>
        </a>
        <a
          href="/contact"
          :class="['relative hover:opacity-80 transition-opacity', isContactActive && 'active-link']"
        >
          Contact
          <span v-if="isContactActive" class="absolute left-0 right-0 -bottom-1 h-px bg-white"></span>
        </a>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface Props {
  currentPath?: string;
}

const props = withDefaults(defineProps<Props>(), {
  currentPath: '/'
});

const isProjectsActive = computed(() => {
  return props.currentPath === '/projects' || props.currentPath.startsWith('/projects/') ||
         props.currentPath === '/upling' || props.currentPath === '/orbit' ||
         props.currentPath === '/fnac-campaigns' || props.currentPath === '/board-game';
});

const isAboutActive = computed(() => {
  return props.currentPath === '/about';
});

const isContactActive = computed(() => {
  return props.currentPath === '/contact';
});
</script>
