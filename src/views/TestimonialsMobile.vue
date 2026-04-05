<script setup>
import FramedMainSection from '@/layouts/FramedMainSection.vue';
import testimonials from '@/data/testimonials.json';
import TestimonialWriterCard from '@/components/TestimonialWriterCard.vue';
</script>

<template>
    <FramedMainSection id="testimonials" class="min-h-[100dvh] flex relative">
        <div class="h-full w-full relative rounded-4xl text-black flex justify-center items-end text-center p-4 overflow-hidden shadow-sm">
            <div class="absolute h-full w-full inset-0 bg-[url('/backgrounds/testimonials_bg.png')] bg-cover -z-10"></div>
            <div class="flex h-full flex-col pt-[6dvw] md:flex-row">

                <div v-for="(testimonial, i) in testimonials" :key="i"
                    class="h-fit flex-1 p-4 flex flex-col items-start cursor-default text-left">
                    <TestimonialWriterCard 
                            :writerImage="testimonial.writer_image" 
                            :writerPosition="testimonial.writer_position" 
                            :starsCount="testimonial.stars" 
                            :isDarkMode="false"
                            />
                    <p class="pt-2 text-justify">{{ testimonial.description }}</p>
                </div>
            </div>
        </div>
    </FramedMainSection>
</template>
