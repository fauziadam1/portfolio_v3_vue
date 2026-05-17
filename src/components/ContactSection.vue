<script setup>
import { DATA } from "@/data/resume";
import FlickeringGrid from "./FlickeringGrid.vue";
</script>

<template>
  <div class="border rounded-xl p-10 relative">
    <div class="absolute -top-4 border bg-primary z-10 rounded-xl px-4 py-1 left-1/2 -translate-x-1/2">
      <span class="text-background text-sm font-medium">Contact</span>
    </div>
    <div class="absolute inset-0 top-0 left-0 right-0 h-1/2 rounded-xl overflow-hidden">
      <FlickeringGrid class="h-full w-full [mask-image:linear-gradient(to_bottom,black,transparent)]" :square-size="2" :grid-gap="2" />
    </div>
    <div class="relative flex flex-col items-center gap-4 text-center">
      <h2 class="text-3xl font-bold tracking-tighter sm:text-5xl">Get in Touch</h2>
      <p class="mx-auto max-w-lg text-muted-foreground text-balance">
        Want to chat? Just shoot me a dm
        <a :href="DATA.contact.social.Instagram.url" target="_blank" rel="noopener noreferrer" class="text-blue-500 hover:underline underline-offset-4 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 rounded-sm">
          with a direct question on Instagram
        </a>
        and I'll respond whenever I can. I will ignore all soliciting.
      </p>
    </div>
  </div>
</template>
