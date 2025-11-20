<template>
  <div class="grid md:grid-cols-2 gap-8 mt-12">
    <div>
      <p class="text-xl font-semibold mb-2.5">Problem</p>
      <p class="opacity-90">
        <slot name="problem" />
      </p>
    </div>
    <div>
      <p class="text-xl font-semibold mb-2.5">Solution</p>
      <p class="opacity-90">
        <slot name="solution" />
      </p>
    </div>
  </div>
</template>

<script setup lang="ts"></script>
