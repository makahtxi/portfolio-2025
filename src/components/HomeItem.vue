<template>
  <div
    class="cursor-pointer h-fit w-6/12 border-[#575757] hover:bg-stone-200"
    @mouseenter="active = true"
    @mouseleave="active = false"
  >
    <a :href="href" class="w-full">
      <p class="cursor-pointer text-2xl font-medium p-3 text-center xl:text-left align-middle">
        {{ name }}
      </p>
      <div
        :class="[
          'bg-[#575757] h-1 m-0 transition-all duration-300',
          active ? 'w-full p-[2px]' : 'w-0'
        ]"
      />
    </a>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Props {
  name: string;
  href: string;
}

const props = withDefaults(defineProps<Props>(), {
  name: 'title',
  href: '#'
});

const active = ref(false);
</script>
