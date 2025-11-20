<template>
  <div
    class="bg-[#212121] box-border flex flex-col gap-4 items-start pb-12 pt-8 px-8 rounded-[8px] w-full"
  >
    <div
      class="flex flex-col gap-2 items-start  not-italic text-md text-left"
    >
      <p class="font-bold  text-[#e36030] shrink-0">
        Problem:
      </p>
      <p class="font-light  text-[#f4f4f4] w-full shrink-0">
        {{ problemDescription }}
      </p>
    </div>
    <div
      class="flex flex-col gap-2 items-start not-italic text-md text-left"
    >
      <p class="font-bold  text-[#67d2d4]  shrink-0">
        Changes:
      </p>
      <p class="font-light  text-[#f4f4f4] w-full shrink-0">
        {{ changesDescription }}
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  problemDescription: string;
  changesDescription: string;
}

defineProps<Props>();
</script>
