<script setup>
import FramedMainSection from '@/layouts/FramedMainSection.vue';
import stories from '@/data/about-me.json';
</script>

<template>
  <FramedMainSection id="about-me" class="min-h-[100dvh] flex items-center relative">
    <div class="h-full w-full relative rounded-4xl text-neutral-900 flex justify-center items-end text-center px-4 overflow-hidden">
      <div class="absolute h-full w-full top-0 left-0 bg-[url('/backgrounds/about_me_subtle.png')] bg-cover bg-center -z-10"></div>
      <div class="flex h-full flex-col pt-[6dvw] md:flex-row overflow-y-auto">
        <div v-for="(story, i) in stories" :key="i"
          class="h-fit flex-1 p-4 flex flex-col items-start cursor-default text-left gap-2 mb-10 last:mb-0">
          <div class="rounded-2xl object-contain aspect-video w-full overflow-hidden shadow-lg">
            <img :src="story.image" alt="" class="h-full w-full object-cover" />
          </div>
          <span class="font-rubik text-neutral-400 text-sm italic">{{ story.when }}</span>
          <h1 class="font-rubik text-xl italic font-bold">{{ story.description }}</h1>
        </div>
      </div>
    </div>
  </FramedMainSection>
</template>
