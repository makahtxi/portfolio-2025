<template>
  <div class="flex flex-col md:flex-row justify-between h-fit mx-auto pt-28">
    <div class="flex flex-col w-full md:w-[45%]">
      <div class="flex flex-col">
        <span class="text-2xl font-medium text-orbit-purple-light m-0">{{ label }}</span>
        <h1 class="text-[44px] font-bold m-0">{{ title }}</h1>
      </div>

      <div class="flex justify-start gap-12 my-5 font-medium text-base flex-wrap">
        <span v-for="tag in tags" :key="tag">{{ tag }}</span>
      </div>

      <div class="flex gap-5 my-5">
        <slot name="properties">
          <div v-for="prop in properties" :key="prop.label">
            <p class="font-bold">{{ prop.label }}</p>
            <p>{{ prop.value }}</p>
          </div>
        </slot>
      </div>
    </div>

    <img :src="thumbnail" :alt="thumbnailAlt" class="w-full md:w-1/2 flex justify-center items-center" />
  </div>
</template>

<script setup lang="ts">
interface Property {
  label: string;
  value: string;
}

interface Props {
  label?: string;
  title: string;
  tags: string[];
  thumbnail: string;
  thumbnailAlt?: string;
  properties?: Property[];
}

withDefaults(defineProps<Props>(), {
  label: 'Case Study',
  thumbnailAlt: 'Case Study Thumbnail',
  properties: () => []
});
</script>
