<template>
  <article class="flex w-[40%] bg-[#1e1e1e] flex-col rounded-sm">
    <a :href="href">
      <div class="flex text-white items-end gap-4 px-2 py-2">
        <h2 class="text-lg font-semibold ">{{ name }}</h2>
        <span class="text-sm font-light ">{{ tags }}</span>
      </div>
      <img class="rounded-b-sm" :src="img" :alt="name" />
      
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
