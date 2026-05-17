<script setup>
import { Moon, Sun } from "@lucide/vue";
import { onMounted, ref } from "vue";
import { DATA } from "@/data/resume";
import Icon from "./Icon.vue";

const isDark = ref(false);

function applyTheme(value) {
  isDark.value = value;
  document.documentElement.classList.toggle("dark", value);
  localStorage.setItem("theme", value ? "dark" : "light");
}

onMounted(() => {
  applyTheme(localStorage.getItem("theme") === "dark");
});
</script>

<template>
  <div class="pointer-events-none fixed inset-x-0 bottom-4 z-30">
    <div class="z-50 pointer-events-auto relative h-14 p-2 w-fit mx-auto flex gap-2 border bg-card/90 backdrop-blur-3xl shadow-[0_0_10px_3px] shadow-primary/5 items-end justify-center overflow-visible rounded-full">
      <a
        v-for="item in DATA.navbar"
        :key="item.href"
        :href="item.href"
        :target="item.href.startsWith('http') ? '_blank' : undefined"
        :rel="item.href.startsWith('http') ? 'noopener noreferrer' : undefined"
        class="group relative"
      >
        <span class="absolute -top-11 left-1/2 hidden -translate-x-1/2 rounded-xl bg-primary px-4 py-2 text-sm text-primary-foreground shadow-[0_10px_40px_-10px_rgba(0,0,0,0.3)] group-hover:block">
          {{ item.label }}
        </span>
        <span class="relative flex aspect-square items-center justify-center rounded-full shrink-0 size-10 bg-background p-2 text-muted-foreground hover:text-foreground hover:bg-muted backdrop-blur-3xl border border-border transition-all hover:size-[60px]">
          <Icon :name="item.icon" class="size-full rounded-sm overflow-hidden object-contain" />
        </span>
      </a>
      <div class="h-2/3 m-auto w-px bg-border" />
      <a
        v-for="[name, social] in Object.entries(DATA.contact.social).filter(([, value]) => value.navbar)"
        :key="name"
        :href="social.url"
        :target="social.url.startsWith('http') ? '_blank' : undefined"
        :rel="social.url.startsWith('http') ? 'noopener noreferrer' : undefined"
        class="group relative"
      >
        <span class="absolute -top-11 left-1/2 hidden -translate-x-1/2 rounded-xl bg-primary px-4 py-2 text-sm text-primary-foreground shadow-[0_10px_40px_-10px_rgba(0,0,0,0.3)] group-hover:block">
          {{ name }}
        </span>
        <span class="relative flex aspect-square items-center justify-center rounded-full shrink-0 size-10 bg-background p-2 text-muted-foreground hover:text-foreground hover:bg-muted backdrop-blur-3xl border border-border transition-all hover:size-[60px]">
          <Icon :name="social.icon" class="size-full rounded-sm overflow-hidden object-contain" />
        </span>
      </a>
      <div class="h-2/3 m-auto w-px bg-border" />
      <button
        type="button"
        class="group relative flex aspect-square items-center justify-center rounded-full shrink-0 size-10 bg-background p-2 text-muted-foreground hover:text-foreground hover:bg-muted backdrop-blur-3xl border border-border transition-all hover:size-[60px] cursor-pointer"
        @click="applyTheme(!isDark)"
      >
        <span class="absolute -top-11 left-1/2 hidden -translate-x-1/2 rounded-xl bg-primary px-4 py-2 text-sm text-primary-foreground shadow-[0_10px_40px_-10px_rgba(0,0,0,0.3)] group-hover:block">
          Theme
        </span>
        <Sun v-if="!isDark" class="size-full" />
        <Moon v-else class="size-full" />
      </button>
    </div>
  </div>
</template>
