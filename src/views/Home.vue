<script setup>
import { ref, onMounted } from 'vue';
import TextAnim from '@/components/TextAnim.vue';
import FramedMainSection from '@/layouts/FramedMainSection.vue';

const frameRef = ref(null);
const containerRef = ref(null);

onMounted(() => {
  containerRef.value = frameRef.value.sectionRef;
});
</script>

<template>
  <FramedMainSection
    ref="frameRef"
    id="gokul kannan ganesamoorthy"
    class="h-dvh"
  >
    <div
      class="h-full w-full bg-cover bg-position-[center_40%] rounded-4xl bg-[url('/backgrounds/hero_bg.png')] flex flex-col justify-center items-center text-center overflow-hidden"
    >
      <!-- Visually Hidden H1 for SEO -->
      <h1 class="sr-only">Gokul Kannan Ganesamoorthy | Creative Fullstack Developer & Designer</h1>
      <div
        class="text-neutral-900 font-rubik uppercase text-[10dvw] xl:text-[13dvh] leading-none flex flex-col justify-center items-center"
      >
        <p class="flex h-[8.4dvw] xl:h-[11dvh]">In order</p>

        <p class="flex h-[8.4dvw] xl:h-[11dvh] overflow-hidden">
          <span class="standard-text">to </span>
          <TextAnim
            v-if="containerRef"
            :texts="['Build', 'Scale', 'Craft']"
            :container="containerRef"
            :duration="2.5"
            :class="'text-red-custom'"
          />
        </p>

        <p class="flex h-[8.4dvw] xl:h-[11dvh]">the future</p>
        <p class="flex h-[8.4dvw] xl:h-[11dvh]">from ideas</p>
        <p class="flex h-[8.4dvw] xl:h-[11dvh]">to reality.</p>
      </div>
    </div>
  </FramedMainSection>
</template>
