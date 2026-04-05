<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { AnimatedComponent } from '@/services/AnimatedComponent'
import { useCursorContext } from '@/composables/useCursorContext';
import { useWindowContext } from '@/composables/useWindowContext';

const { getPositions } = useCursorContext();
const { md } = useWindowContext();


const rootRef = ref();
const component = ref();
const parallaxItems = ref([]);
const autoAnimDegree = ref(0);

const updatePosition = () => {
  const rootRect = rootRef.value.getBoundingClientRect();
  const cur = getPositions();
  const relativeCursorX = rootRect.width / 2 + rootRect.left;
  const relativeCursorY = rootRect.height / 2 + rootRect.top;

  // Always increment the autonomous motion loop
  autoAnimDegree.value = (autoAnimDegree.value + 0.005) % 360;
  const hyp = 300;
  const autoX = hyp * Math.cos(autoAnimDegree.value * 1.5);
  const autoY = hyp * Math.sin(autoAnimDegree.value);

  parallaxItems.value.forEach((el) => {
    const multiplicator = parseFloat(el.dataset.parallaxValue) || 0.1;
    let x;
    let y;

    if (!md.value) {
      // Mobile: Pure autonomous looping motion
      x = autoX * -multiplicator;
      y = autoY * -multiplicator;
    } else {
      // PC: Combine autonomous motion + subtle cursor follow
      const dx = cur.x - relativeCursorX;
      const dy = cur.y - relativeCursorY;
      const cursorX = -(dx * multiplicator * 2) / Math.log(Math.abs(dx) + 2);
      const cursorY = -(dy * multiplicator * 2) / Math.log(Math.abs(dy) + 2);

      // Blend auto-motion and cursor-follow
      x = cursorX + (autoX * multiplicator * 0.5);
      y = cursorY + (autoY * multiplicator * 0.5);
    }

    el.style.transform = `translateX(${x}px) translateY(${y}px)`;
  });
};

onMounted(() => {
  parallaxItems.value = Array.from(rootRef.value.getElementsByClassName("parallax"));
  component.value = new AnimatedComponent(rootRef.value);
  component.value.tick = updatePosition;
  component.value.autoAnimate();
})

onBeforeUnmount(() => {
  component.value.reset();
})
</script>

<template>
  <div ref="rootRef" class="parallax-wrapper h-full w-full">
    <slot></slot>
  </div>
</template>
