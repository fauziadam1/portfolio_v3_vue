<script setup>
import { DATA } from "@/data/resume";
import ProjectCard from "./ProjectCard.vue";
</script>

<template>
  <section id="projects">
    <div class="flex min-h-0 flex-col gap-y-8">
      <div class="flex flex-col gap-y-4 items-center justify-center">
        <div class="flex items-center w-full">
          <div class="flex-1 h-px bg-linear-to-r from-transparent from-5% via-border via-95% to-transparent" />
          <div class="border bg-primary z-10 rounded-xl px-4 py-1">
            <span class="text-background text-sm font-medium">My Projects</span>
          </div>
          <div class="flex-1 h-px bg-linear-to-l from-transparent from-5% via-border via-95% to-transparent" />
        </div>
        <div class="flex flex-col gap-y-3 items-center justify-center">
          <h2 class="text-3xl font-bold tracking-tighter sm:text-4xl">Check out my latest work</h2>
          <p class="text-muted-foreground md:text-lg/relaxed lg:text-base/relaxed xl:text-lg/relaxed text-balance text-center">
            I've worked on a variety of projects, from simple websites to complex web applications and some website design. Here are a few of my favorites.
          </p>
        </div>
      </div>
      <div class="grid grid-cols-1 gap-3 sm:grid-cols-2 max-w-200 mx-auto auto-rows-fr">
        <div v-for="(project, id) in DATA.projects" :key="project.title" class="h-full blur-fade" :style="{ animationDelay: `${0.48 + id * 0.05}s` }">
          <ProjectCard
            :href="project.href"
            :title="project.title"
            :description="project.description"
            :dates="project.dates"
            :tags="project.technologies"
            :image="project.image"
            :video="project.video"
            :links="project.links"
          />
        </div>
      </div>
    </div>
  </section>
</template>
