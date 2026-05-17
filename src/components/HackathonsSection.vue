<script setup>
import { DATA } from "@/data/resume";
import Icon from "./Icon.vue";
</script>

<template>
  <section id="hackathons" class="overflow-hidden">
    <div class="flex min-h-0 flex-col gap-y-8 w-full">
      <div class="flex flex-col gap-y-4 items-center justify-center">
        <div class="flex items-center w-full">
          <div class="flex-1 h-px bg-linear-to-r from-transparent from-5% via-border via-95% to-transparent" />
          <div class="border bg-primary z-10 rounded-xl px-4 py-1">
            <span class="text-background text-sm font-medium">Activity</span>
          </div>
          <div class="flex-1 h-px bg-linear-to-l from-transparent from-5% via-border via-95% to-transparent" />
        </div>
        <div class="flex flex-col gap-y-3 items-center justify-center">
          <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">I like to be active</h2>
          <p class="text-muted-foreground md:text-lg/relaxed lg:text-base/relaxed xl:text-lg/relaxed text-balance text-center">
            During my time at school, I attended several webinars, competition, and courses. These activities motivated me to deepen my interest in programming.
          </p>
        </div>
      </div>
      <div class="relative flex flex-col gap-4 p-4 w-full">
        <div class="relative [&>*:last-child_[data-timeline-line]]:hidden space-y-8 w-full">
          <div v-for="hackathon in DATA.hackathons" :key="hackathon.title + hackathon.dates" class="relative w-full flex items-start justify-between gap-10">
            <div class="relative flex w-10 shrink-0 justify-center self-stretch">
              <div data-timeline-line class="absolute left-1/2 top-5 z-0 h-[calc(100%+2rem)] w-px -translate-x-1/2 bg-border" />
              <div class="relative z-20 shrink-0">
                <img v-if="hackathon.image" :src="hackathon.image" :alt="hackathon.title" class="size-10 bg-card z-10 shrink-0 overflow-hidden p-1 border rounded-full shadow ring-2 ring-border object-contain flex-none" />
                <div v-else class="size-10 bg-card z-10 shrink-0 overflow-hidden p-1 border rounded-full shadow ring-2 ring-border flex-none" />
              </div>
            </div>
            <div class="flex flex-1 flex-col justify-start gap-2 min-w-0">
              <time class="text-xs text-muted-foreground">{{ hackathon.dates }}</time>
              <h3 class="font-semibold leading-none">{{ hackathon.title }}</h3>
              <p class="text-sm text-muted-foreground">{{ hackathon.location }}</p>
              <p class="text-sm text-muted-foreground leading-relaxed wrap-break-word">{{ hackathon.description }}</p>
              <div v-if="hackathon.links?.length" class="mt-1 flex flex-row flex-wrap items-start gap-2">
                <a v-for="(link, idx) in hackathon.links" :key="idx" :href="link.href" target="_blank" rel="noopener noreferrer">
                  <div class="inline-flex items-center rounded-md border px-2.5 py-0.5 font-semibold transition-colors focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 border-transparent shadow flex gap-1.5 text-xs bg-primary text-primary-foreground">
                    <Icon :name="link.icon" class="h-4 w-4" />
                    {{ link.title }}
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
