<script setup>
import ArrowIcon from '@/icons/ArrowIcon.vue'

const props = defineProps({
  open: { type: Boolean, default: false }
})

const emit = defineEmits(['toggle', 'hover', 'leave']);
</script>

<template>
  <div class="w-full flex-col border-t border-black/10 last:border-b-0 group transition-colors duration-500 hover:bg-black/5 cursor-pointer relative"
       :class="props.open ? 'bg-black/5' : ''"
       @mouseover="emit('hover')" @mouseleave="emit('leave')">
    
    <div class="py-8 md:py-12 w-full flex justify-between items-center transition-all px-4 xl:px-12"
         @click="emit('toggle')">
      
      <!-- header slot container -->
      <div class="z-10 w-full flex justify-between items-center text-black">
        <slot name="header"></slot>
        
        <!-- Toggle Icon (animated arrow in a modern bordered circle) -->
        <div class="w-10 h-10 md:w-14 md:h-14 flex-shrink-0 flex justify-center items-center rounded-full border border-black/20 transition-all duration-500 group-hover:border-black group-hover:scale-110 ml-4"
             :class="props.open ? 'bg-black text-white border-transparent' : 'bg-transparent text-black'">
          <ArrowIcon class="transition-transform duration-700 w-4 h-4 md:w-5 md:h-5" :class="props.open ? 'rotate-[270deg] invert' : 'rotate-90 filter-none'" />
        </div>
      </div>
    </div>

    <!-- Smooth grid height transition for the accordion content -->
    <div class="grid transition-[grid-template-rows] duration-700 ease-in-out overflow-hidden px-4 xl:px-12"
         :style="props.open ? 'grid-template-rows: 1fr;' : 'grid-template-rows: 0fr;'">
      <div class="min-h-0">
        <slot name="content"></slot>
      </div>
    </div>
  </div>
</template>
