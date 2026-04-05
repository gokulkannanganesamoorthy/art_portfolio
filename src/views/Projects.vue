<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';
import FramedMainSection from '@/layouts/FramedMainSection.vue';
import projects from '@/data/projects.json';
import ArrowIcon from '@/icons/ArrowIcon.vue';
import { useScrollContext } from '@/composables/useScrollContext';

const { registerSection, unregisterSection } = useScrollContext();
const frameRef = ref();
const activeIndex = ref(0); // Default first one open

const toggleProject = (index) => {
  if (activeIndex.value === index) {
    activeIndex.value = -1; // Close if already open
  } else {
    activeIndex.value = index;
  }
};

onMounted(async () => {
  await nextTick();
  if (frameRef.value) {
    registerSection('projects', frameRef.value.sectionRef);
  }
});

onBeforeUnmount(() => {
  unregisterSection('projects');
});
</script>

<template>
  <FramedMainSection
    ref="frameRef"
    id="projects"
    class="min-h-[100dvh] flex flex-col h-auto relative bg-white overflow-hidden pb-10"
  >
    <!-- Oil Pastel Background Layer -->
    <div
      class="absolute inset-0 bg-[url('/backgrounds/projects_bg.png')] bg-cover bg-center opacity-[0.15] pointer-events-none rounded-4xl"
    ></div>
    <!-- Header -->
    <div class="w-full max-w-7xl mx-auto px-6 md:px-12 pt-32 mb-20">
      <h2
        class="text-neutral-400 font-rubik text-xs uppercase tracking-[0.8em] mb-4 text-center md:text-left"
      >
        Portfolio
      </h2>
      <h1
        class="text-neutral-900 font-rubik font-bold text-5xl md:text-8xl uppercase tracking-tighter leading-none text-center md:text-left"
      >
        Selected <span class="text-red-custom">Projects</span>.
      </h1>
    </div>

    <!-- Interactive Accordion Stack -->
    <div class="w-full max-w-7xl mx-auto px-4 md:px-12 flex flex-col pt-10">
      <div
        v-for="(project, pi) in projects"
        :key="pi"
        class="w-full border-t border-neutral-100 last:border-b transition-colors duration-500 overflow-hidden"
        :class="
          activeIndex === pi ? 'bg-neutral-50/30' : 'hover:bg-neutral-50/50'
        "
      >
        <!-- Accordion Header ("The Dropdown Bar") -->
        <div
          class="py-10 md:py-16 w-full flex justify-between items-center cursor-pointer px-4 md:px-10 group"
          @click="toggleProject(pi)"
        >
          <div class="flex items-center gap-6 md:gap-12">
            <span
              class="text-neutral-300 font-rubik text-xs md:text-sm font-bold tracking-widest italic"
              >0{{ pi + 1 }}.</span
            >
            <h2
              class="text-neutral-900 font-rubik font-bold text-2xl md:text-5xl uppercase tracking-tighter group-hover:translate-x-2 transition-transform duration-500"
              :class="activeIndex === pi ? 'text-red-custom' : ''"
            >
              {{ project.title }}
            </h2>
          </div>

          <!-- Modern Toggle Icon -->
          <div
            class="w-10 h-10 md:w-16 md:h-16 flex-shrink-0 flex justify-center items-center rounded-full border border-neutral-200 transition-all duration-500 group-hover:border-neutral-900 group-hover:scale-110"
            :class="
              activeIndex === pi
                ? 'bg-neutral-900 border-transparent shadow-lg'
                : ''
            "
          >
            <ArrowIcon
              class="transition-transform duration-700 w-4 h-4 md:w-5 md:h-5"
              :class="
                activeIndex === pi
                  ? 'rotate-[270deg] text-white'
                  : 'rotate-90 text-neutral-300 group-hover:text-neutral-900'
              "
            />
          </div>
        </div>

        <!-- Animated Content Reveal -->
        <div
          class="grid transition-[grid-template-rows] duration-700 ease-in-out px-4 md:px-10"
          :style="
            activeIndex === pi
              ? 'grid-template-rows: 1fr;'
              : 'grid-template-rows: 0fr;'
          "
        >
          <div class="min-h-0">
            <div
              class="flex flex-col md:flex-row items-center gap-12 pb-20 pt-4"
            >
              <!-- Large Hero Visual -->
              <div
                class="w-full md:w-3/5 aspect-video rounded-[2rem] overflow-hidden shadow-2xl relative group/img"
              >
                <img
                  :src="project.background"
                  alt=""
                  class="w-full h-full object-cover transition-transform duration-1000 group-hover/img:scale-110"
                />
                <div
                  class="absolute inset-0 bg-neutral-900/10 opacity-0 group-hover/img:opacity-100 transition-opacity duration-700"
                ></div>
              </div>

              <!-- Project Details -->
              <div class="w-full md:w-2/5 flex flex-col justify-center">
                <p
                  class="text-neutral-500 font-light text-lg md:text-xl leading-relaxed mb-10 max-w-sm text-center md:text-left"
                >
                  {{ project.description }}
                </p>

                <a
                  :href="project.link"
                  target="_blank"
                  class="group/btn relative w-fit py-4 px-10 bg-neutral-900 text-white rounded-full font-bold uppercase tracking-[0.2em] text-[10px] transition-all hover:bg-red-custom hover:scale-105 active:scale-95 flex items-center gap-4 mx-auto md:mx-0"
                >
                  <span>Explore Project</span>
                  <div
                    class="w-1.5 h-1.5 bg-white rounded-full animate-pulse"
                  ></div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Section Footer -->
    <div class="mt-10 w-full flex flex-col items-center">
      <div class="w-px h-24 bg-neutral-100"></div>
      <p
        class="mt-12 text-neutral-300 font-rubik text-[8px] uppercase tracking-[1em]"
      >
        Building More
      </p>
    </div>
  </FramedMainSection>
</template>

<style scoped>
.text-red-custom {
  color: #ae0001;
}

@keyframes pulse-dot {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.5);
    opacity: 0.5;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
