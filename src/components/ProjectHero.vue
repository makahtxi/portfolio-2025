<template>
  <div class="flex flex-col md:flex-row justify-between h-fit mx-auto pt-28">
    <div class="flex flex-col w-full md:w-[45%]">
      <div class="flex flex-col">
        <span :class="['text-2xl font-medium m-0', categoryColorClass]">
          {{ categoryLabel }}
        </span>
        <h1 class="text-[44px] font-bold m-0" v-html="title"></h1>
      </div>

      <div class="flex justify-start gap-6 my-5 font-medium text-base flex-wrap">
        <span v-for="tag in tags" :key="tag">{{ tag }}</span>
      </div>

      <div class="flex gap-5 my-5">
        <div>
          <p class="font-bold">Year</p>
          <p>{{ year }}</p>
        </div>
        <div>
          <p class="font-bold">Project</p>
          <p>{{ projectName }}</p>
        </div>
      </div>
    </div>

    <img
      v-if="heroImage"
      :src="heroImage"
      :alt="heroImageAlt"
      class="w-full md:w-1/2 flex justify-center items-center rounded-2xl"
    />
  </div>

  <slot />
</template>

<script setup lang="ts">
import { computed } from 'vue';

type ProjectType = 'case-study' | 'showcase' | 'branding';

interface Props {
  type: ProjectType;
  title: string;
  tags: string[];
  year: string;
  projectName: string;
  heroImage?: string;
  heroImageAlt?: string;
}

const props = defineProps<Props>();

const categoryLabel = computed(() => {
  const labels: Record<ProjectType, string> = {
    'case-study': 'Case Study',
    'showcase': 'Showcase',
    'branding': 'Branding'
  };
  return labels[props.type];
});

const categoryColorClass = computed(() => {
  return props.type === 'showcase'
    ? 'text-[#96f9dd]'
    : 'text-orbit-purple-light';
});
</script>
