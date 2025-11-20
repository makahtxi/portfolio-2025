<template>
  <input
    :type="type"
    :placeholder="placeholder"
    :value="modelValue"
    @input="$emit('update:modelValue', ($event.target as HTMLInputElement).value)"
    class="my-4 w-3/5 px-4 py-4 rounded-[10px] text-base text-white bg-orbit-purple-dark border-2 border-orbit-purple-dark font-sans focus:outline-none focus:border-orbit-purple"
  />
</template>

<script setup lang="ts">
interface Props {
  type?: string;
  placeholder?: string;
  modelValue?: string;
}

withDefaults(defineProps<Props>(), {
  type: 'text',
  placeholder: '',
  modelValue: ''
});

defineEmits<{
  'update:modelValue': [value: string]
}>();
</script>
