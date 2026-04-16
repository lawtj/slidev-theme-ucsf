<script setup lang="ts">
const props = defineProps<{
  active: 1 | 2 | 3
}>()

const sectionColors: Record<number, string> = {
  1: '#16A0AC', // C3 Teal
  2: '#006BE9', // A3 CTA Blue
  3: '#A238BA', // G3 Violet
}
</script>

<template>
  <div class="absolute top-5 right-6 flex gap-2 z-10">
    <div
      v-for="n in [1, 2, 3]"
      :key="n"
      class="w-2.5 h-2.5 rounded-full transition-colors duration-300"
      :style="{ backgroundColor: n === active ? sectionColors[n] : '#d1d5db' }"
    />
  </div>
</template>
