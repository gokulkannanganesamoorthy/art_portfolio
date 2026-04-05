<script setup>
import FramedMainSection from '@/layouts/FramedMainSection.vue';
import awards from '@/data/awards.json';
import Parallax from '@/components/Parallax.vue';
</script>

<template>
     <FramedMainSection id="awards" class="h-dvh">
        <Parallax>
            <div class="h-full w-full relative overflow-hidden rounded-4xl text-neutral-900 flex flex-col justify-start md:justify-end items-center text-center p-4 pt-20 md:pt-4">
                <!-- Visually Hidden H1 for SEO -->
                <h1 class="sr-only">Awards & Recognition | Gokul Kannan Ganesamoorthy</h1>
                <!-- Subtle Oil Pastel Background Layer -->
                <div class="absolute inset-0 bg-[url('/backgrounds/awards_bg_subtle.png')] bg-cover bg-center -z-10"></div>
                
                <!-- The "Hand Thing" (Trophy) on Loop -->
                <div class="absolute h-full w-full top-0 left-0 -z-10 overflow-visible pointer-events-none">
                    <img src="/awards/trophy.png" alt="" data-parallax-value=".15" class="parallax w-full absolute scale-200 -bottom-1/12 sm:scale-125 md:scale-150 lg:scale-125 lg:-bottom-1/3">
                </div>

                <div class="flex flex-col md:flex-row max-w-7xl mx-auto w-full">
                    <div v-for="award in awards" :key="award.title" class="h-fit flex-1 p-8 flex flex-col items-start cursor-default text-left group">
                        <span class="font-rubik text-neutral-400 text-xs tracking-widest uppercase mb-2">{{award.date}}</span>
                        <h2 class="font-rubik text-2xl font-bold uppercase tracking-tighter mb-4 group-hover:text-red-custom transition-colors duration-500">{{award.title}}</h2>
                        <p class="text-neutral-600 font-light leading-relaxed">{{award.description}}</p>
                        <div class="w-12 h-px bg-neutral-200 mt-6 group-hover:w-full transition-all duration-700"></div>
                    </div>
                </div>
            </div>
        </Parallax>
    </FramedMainSection>
</template>
