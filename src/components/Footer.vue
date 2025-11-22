<template>
  <footer class="bg-[#1e1e1e] flex flex-col gap-2.5 py-4 w-full">
    <div class="max-w-[1100px] w-full mx-auto px-4 flex items-start justify-between">
      <!-- Copyright Section -->
      <div class="flex flex-col gap-1 items-start justify-center">
        <div class="text-white text-sm font-normal whitespace-pre-line">
          <p class="mb-0">© 2025 Pedro Botica</p>
          <p>UX Designer</p>
        </div>
      </div>

      <!-- Links Section -->
      <div class="flex gap-14 items-start justify-end w-[521.5px]">
        <!-- Sitemap -->
        <div class="flex flex-col gap-1.5 items-start text-white">
          <p class="font-bold text-base mb-0">Sitemap</p>
          <a href="/" class="text-sm hover:opacity-80 transition-opacity">Homepage</a>
          <a href="/projects" class="text-sm hover:opacity-80 transition-opacity">Projects</a>
          <a href="/about" class="text-sm hover:opacity-80 transition-opacity">About</a>
          <a href="/contact" class="text-sm hover:opacity-80 transition-opacity">Contact</a>
        </div>

        <!-- Other Links -->
        <div class="flex flex-col gap-1.5 items-start">
          <p class="font-bold text-base text-white mb-0">Other Links</p>
          <a
            href="https://www.linkedin.com/in/pedro-botica-0096761aa/"
            target="_blank"
            rel="noopener noreferrer"
            class="flex gap-1.5 items-center text-white text-sm hover:opacity-80 transition-opacity"
          >
            <span>LinkedIn</span>
            <svg width="8" height="8" viewBox="0 0 8 8" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M7 1L1 7M7 1H1M7 1V7" stroke="white" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </a>
          <a
            href="/resume"
            class="text-white text-sm hover:opacity-80 transition-opacity"
          >
            Resume
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
// Footer component - no props needed
</script>
