<script setup>
import { ArrowUpRight } from "@lucide/vue";
import Icon from "./Icon.vue";
import MarkdownText from "./MarkdownText.vue";

defineProps({
  title: { type: String, required: true },
  href: { type: String, default: "" },
  description: { type: String, required: true },
  dates: { type: String, required: true },
  tags: { type: Array, default: () => [] },
  image: { type: String, default: "" },
  video: { type: String, default: "" },
  links: { type: Array, default: () => [] },
});
</script>

<template>
  <div class="flex flex-col h-full border border-border rounded-xl overflow-hidden hover:ring-2 cursor-pointer hover:ring-muted transition-all duration-200">
    <div class="relative shrink-0">
      <a :href="href || '#'" target="_blank" rel="noopener noreferrer" class="block">
        <video v-if="video" :src="video" autoplay loop muted playsinline class="w-full h-48 object-cover" />
        <img v-else-if="image" :src="image" :alt="title" class="w-full h-48 object-cover" />
        <div v-else class="w-full h-48 bg-muted" />
      </a>
      <div v-if="links?.length" class="absolute top-2 right-2 flex flex-wrap gap-2">
        <a v-for="(link, idx) in links" :key="idx" :href="link.href" target="_blank" rel="noopener noreferrer">
          <div class="inline-flex items-center rounded-md border px-2.5 py-0.5 font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 border-transparent shadow flex gap-1.5 text-xs bg-black text-white hover:bg-black/90">
            <Icon :name="link.icon" class="size-3" />
            {{ link.type }}
          </div>
        </a>
      </div>
    </div>
    <div class="p-6 flex flex-col gap-3 flex-1">
      <div class="flex items-start justify-between gap-2">
        <div class="flex flex-col gap-1">
          <h3 class="font-semibold">{{ title }}</h3>
          <time class="text-xs text-muted-foreground">{{ dates }}</time>
        </div>
        <a :href="href || '#'" target="_blank" rel="noopener noreferrer" class="text-muted-foreground hover:text-foreground transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2 rounded-sm" :aria-label="`Open ${title}`">
          <ArrowUpRight class="h-4 w-4" aria-hidden="true" />
        </a>
      </div>
      <div class="text-xs flex-1 prose max-w-full text-pretty font-sans leading-relaxed text-muted-foreground dark:prose-invert">
        <MarkdownText :text="description" />
      </div>
      <div v-if="tags.length" class="flex flex-wrap gap-1 mt-auto">
        <div v-for="tag in tags" :key="tag" class="inline-flex items-center rounded-md transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 text-[11px] font-medium border border-border h-6 w-fit px-2">
          {{ tag }}
        </div>
      </div>
    </div>
  </div>
</template>
