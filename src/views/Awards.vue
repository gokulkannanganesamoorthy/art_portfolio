<script setup>
import FramedMainSection from '@/layouts/FramedMainSection.vue';
import awards from '@/data/awards.json';
import Parallax from '@/components/Parallax.vue';
</script>

<template>
  <FramedMainSection id="awards" class="h-dvh">
    <Parallax>
      <div
        class="h-full w-full relative overflow-hidden rounded-4xl text-neutral-900 flex justify-center items-start md:items-end text-center p-4"
      >
        <!-- Visually Hidden H1 for SEO -->
        <h1 class="sr-only">
          Awards & Recognition | Gokul Kannan Ganesamoorthy
        </h1>
        <div
          class="absolute h-full w-full bg-[url('/backgrounds/awards_bg_subtle.png')] bg-cover top-0 left-0 -z-10 overflow-visible"
        >
          <div
            data-parallax-value=".02"
            class="parallax absolute top-2/5 left-1/2 -translate-x-1/2 -translate-y-1/2 aspect-video w-[130dvw] bg-center bg-cover bg-[url('/awards/clouds.png')]"
          ></div>
          <img
            src="/awards/trophy.png"
            alt="International Trophy"
            data-parallax-value=".15"
            class="parallax w-full absolute scale-200 -bottom-1/12 sm:scale-125 md:scale-150 lg:scale-125 lg:-bottom-1/3"
          />
        </div>
        <div class="flex flex-col md:flex-row max-w-7xl mx-auto w-full">
          <div
            v-for="award in awards"
            :key="award.title"
            class="h-fit flex-1 p-4 flex flex-col items-start cursor-default text-left"
          >
            <span
              class="font-rubik opacity-60 text-xs uppercase tracking-widest mb-1"
              >{{ award.date }}</span
            >
            <h2 class="font-rubik text-xl italic font-bold mb-2">
              {{ award.title }}
            </h2>
            <p class="font-light opacity-80 text-sm leading-relaxed">
              {{ award.description }}
            </p>
          </div>
        </div>
      </div>
    </Parallax>
  </FramedMainSection>
</template>
