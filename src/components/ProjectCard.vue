<template>
  <a :href="link" class="bg-[#333333]/99   gap-12 rounded-xl flex justify-between items-between px-11 py-6 hover:bg-[#212121] hover:cursor-pointer transition-colors no-underline">
    <div class="flex items-center justify-center overflow-hidden shrink-0 h-40 w-40 bg-white rounded-lg">
      <img
        :src="image"
        :alt="imageAlt"
        :class="[
          'w-full h-full object-cover'
        ]"
      />
    </div>
    <div class="flex flex-col gap-2">
      <div class="flex flex-col gap-3">
        <h3 class="text-[28px] font-bold text-[#f4f4f4]">
          {{ title }}
        </h3>
        <p class="text-base text-[#f4f4f4]">
          {{ description }}
        </p>
      </div>
      <span class="text-base text-[#f4f4f4] underline">
        See more
      </span>
    </div>
  </a>
</template>

<script setup lang="ts">
interface Props {
  image: string;
  imageAlt: string;
  title: string;
  description: string;
  link: string;
  imageContain?: boolean;
  trackingClass?: string;
}

withDefaults(defineProps<Props>(), {
  imageContain: false,
  trackingClass: ''
});
</script>
