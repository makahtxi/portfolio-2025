<template>
  <article class="flex w-[40%] flex-col">
    <a :href="href">
      <div class="flex items-end gap-4 mb-2">
        <h2 class="text-lg font-semibold ">{{ name }}</h2>
        <span class="text-sm font-light ">{{ tags }}</span>
      </div>
      <img :src="img" :alt="name" />
      
    </a>
  </article>
</template>

<script setup lang="ts">
interface Props {
  name: string;
  href: string;
  tags: string;
  color: string;
  img: string;
}

withDefaults(defineProps<Props>(), {
  name: 'ProjectName',
  href: '#',
  tags: 'UX/UI, Branding, User Research',
  color: '#000000',
  img: 'src/images/Boaty.png'
});
</script>
