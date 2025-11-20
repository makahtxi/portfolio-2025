<template>
  <a
    :href="href"
    class="group block bg-white rounded-[var(--radius-card)] shadow-md hover:shadow-xl transition-smooth overflow-hidden"
  >
    <div class="aspect-video overflow-hidden">
      <img
        :src="image"
        :alt="title"
        class="w-full h-full object-cover group-hover:scale-105 transition-smooth"
      />
    </div>

    <div class="p-6 space-y-4">
      <div>
        <h2 class="text-2xl font-bold text-orbit-dark mb-2">{{ title }}</h2>
        <p class="text-orbit-dark/70 leading-relaxed">{{ description }}</p>
      </div>

      <div class="flex gap-2 flex-wrap">
        <span
          v-for="tag in tags"
          :key="tag"
          class="px-3 py-1 bg-orbit-light rounded-full text-sm text-orbit-dark"
        >
          {{ tag }}
        </span>
      </div>

      <div class="flex gap-6 text-sm">
        <div v-if="year">
          <span class="font-semibold text-orbit-dark">Year:</span>
          <span class="text-orbit-dark/70 ml-1">{{ year }}</span>
        </div>
        <div v-if="client">
          <span class="font-semibold text-orbit-dark">{{ clientLabel }}:</span>
          <span class="text-orbit-dark/70 ml-1">{{ client }}</span>
        </div>
      </div>

      <div class="flex items-center gap-2 text-orbit-purple font-semibold pt-2">
        <span>View Case Study</span>
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M6 3L11 8L6 13" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>
    </div>
  </a>
</template>

<script setup lang="ts">
interface Props {
  title: string;
  description: string;
  image: string;
  href: string;
  tags: string[];
  year?: string;
  client?: string;
  clientLabel?: string;
}

withDefaults(defineProps<Props>(), {
  clientLabel: 'Client'
});
</script>
