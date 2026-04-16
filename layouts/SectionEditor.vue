
<template>
  <div
    class="absolute left-0 top-50 w-4/5 h-25 rounded-xl shadow-lg p-8 flex flex-col justify-center items-start"
    :style="{ background: gradient }"
  >
    <div class="text-3xl font-bold text-white">
      <slot name="title"/>
    </div>
    <div class="text-xl text-white/80">
      <slot name="subtitle"/>
    </div>
  </div>
  <SectionDots v-if="section" :active="section" />
</template>

<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  section?: 1 | 2 | 3
}>()

const gradients: Record<number, string> = {
  1: 'linear-gradient(to right, #16A0AC, #083B40)', // C3 Teal → deep teal
  2: 'linear-gradient(to right, #006BE9, #001A6B)', // A3 CTA Blue → deep blue (not navy)
  3: 'linear-gradient(to right, #A238BA, #461850)', // G3 Violet → G1 deep purple
}

const gradient = computed(() => gradients[props.section ?? 0] ?? 'linear-gradient(to right, #16A0AC, #083B40)')
</script>
