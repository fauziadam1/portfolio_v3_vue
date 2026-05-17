<script setup>
import { ArrowUpRight } from "@lucide/vue";
import { DATA } from "@/data/resume";
import ContactSection from "@/components/ContactSection.vue";
import FlickeringGrid from "@/components/FlickeringGrid.vue";
import HackathonsSection from "@/components/HackathonsSection.vue";
import Icon from "@/components/Icon.vue";
import MarkdownText from "@/components/MarkdownText.vue";
import Navbar from "@/components/Navbar.vue";
import ProjectsSection from "@/components/ProjectsSection.vue";

const blurDelay = 0.04;
</script>

<template>
  <div class="min-h-screen bg-background font-sans antialiased relative">
    <div class="absolute inset-0 top-0 left-0 right-0 h-25 overflow-hidden z-0">
      <FlickeringGrid class="h-full w-full [mask-image:linear-gradient(to_bottom,black,transparent)]" :square-size="2" :grid-gap="2" />
    </div>
    <div class="relative z-10 max-w-2xl mx-auto py-12 pb-24 sm:py-24 px-6">
      <main class="min-h-dvh flex flex-col gap-14 relative">
        <section id="hero">
          <div class="mx-auto w-full max-w-2xl space-y-8">
            <div class="gap-2 gap-y-6 flex flex-col md:flex-row justify-between">
              <div class="gap-2 flex flex-col order-2 md:order-1">
                <div class="flex blur-fade" :style="{ animationDelay: `${blurDelay}s` }">
                  <span class="inline-block text-3xl font-semibold tracking-tighter sm:text-4xl lg:text-5xl">
                    Hi, I'm {{ DATA.name.split(" ")[0] }}
                  </span>
                </div>
                <div class="flex blur-fade" :style="{ animationDelay: `${blurDelay}s` }">
                  <span class="inline-block text-muted-foreground max-w-120 md:text-md lg:text-lg">
                    {{ DATA.description }}
                  </span>
                </div>
              </div>
              <div class="order-1 md:order-2 blur-fade" :style="{ animationDelay: `${blurDelay}s` }">
                <span class="relative flex h-10 w-10 shrink-0 overflow-hidden size-24 md:size-32 border rounded-full shadow-lg ring-4 ring-muted">
                  <img :src="DATA.avatarUrl" :alt="DATA.name" class="aspect-square h-full w-full object-cover" />
                </span>
              </div>
            </div>
          </div>
        </section>

        <section id="about">
          <div class="flex min-h-0 flex-col gap-y-4">
            <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 3}s` }">
              <h2 class="text-xl font-bold">About</h2>
            </div>
            <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 4}s` }">
              <div class="prose max-w-full text-pretty font-sans leading-relaxed text-muted-foreground dark:prose-invert">
                <MarkdownText :text="DATA.summary" />
              </div>
            </div>
          </div>
        </section>

        <section id="education">
          <div class="flex min-h-0 flex-col gap-y-6">
            <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 7}s` }">
              <h2 class="text-xl font-bold">Education</h2>
            </div>
            <div class="flex flex-col gap-8">
              <div
                v-for="(education, index) in DATA.education"
                :key="education.school"
                class="blur-fade"
                :style="{ animationDelay: `${blurDelay * 8 + index * 0.05}s` }"
              >
                <a :href="education.href" target="_blank" rel="noopener noreferrer" class="flex items-center gap-x-3 justify-between group">
                  <div class="flex items-center gap-x-3 flex-1 min-w-0">
                    <img v-if="education.logoUrl" :src="education.logoUrl" :alt="education.school" class="size-8 md:size-10 p-1 border rounded-full shadow ring-2 ring-border overflow-hidden object-contain flex-none" />
                    <div v-else class="size-8 md:size-10 p-1 border rounded-full shadow ring-2 ring-border bg-muted flex-none" />
                    <div class="flex-1 min-w-0 flex flex-col gap-0.5">
                      <div class="font-semibold leading-none flex items-center gap-2">
                        {{ education.school }}
                        <ArrowUpRight class="h-3.5 w-3.5 text-muted-foreground opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-200" aria-hidden="true" />
                      </div>
                      <div class="font-sans text-sm text-muted-foreground">{{ education.degree }}</div>
                    </div>
                  </div>
                  <div class="flex items-center gap-1 text-xs tabular-nums text-muted-foreground text-right flex-none">
                    <span>{{ education.start }} - {{ education.end }}</span>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </section>

        <section id="skills">
          <div class="flex min-h-0 flex-col gap-y-4">
            <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 9}s` }">
              <h2 class="text-xl font-bold">Skills</h2>
            </div>
            <div class="flex flex-wrap gap-2">
              <div
                v-for="(skill, id) in DATA.skills"
                :key="skill.name"
                class="blur-fade"
                :style="{ animationDelay: `${blurDelay * 10 + id * 0.05}s` }"
              >
                <div class="border bg-background border-border ring-2 ring-border/20 rounded-xl h-8 w-fit px-4 flex items-center gap-2">
                  <Icon :name="skill.icon" class="size-4 rounded overflow-hidden object-contain" />
                  <span class="text-foreground text-sm font-medium">{{ skill.name }}</span>
                </div>
              </div>
            </div>
          </div>
        </section>

        <section id="projects">
          <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 11}s` }">
            <ProjectsSection />
          </div>
        </section>

        <section id="hackathons">
          <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 13}s` }">
            <HackathonsSection />
          </div>
        </section>

        <section id="contact">
          <div class="blur-fade" :style="{ animationDelay: `${blurDelay * 16}s` }">
            <ContactSection />
          </div>
        </section>
      </main>
    </div>
    <Navbar />
  </div>
</template>
