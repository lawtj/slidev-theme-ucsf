<script setup lang="ts">
import { resolveAssetUrl } from '@slidev/client/layoutHelper.ts'

interface Props {
  image?: string
  imageAlt?: string
  presenter?: string
  role?: string
  institution?: string
  date?: string
}

const props = withDefaults(defineProps<Props>(), {
  image: '',
  imageAlt: '',
  presenter: '',
  role: '',
  institution: '',
  date: '',
})
</script>

<template>
  <div class="slidev-layout title-slide h-full relative overflow-hidden">

    <!-- Full-bleed background image -->
    <img
      v-if="image"
      :src="resolveAssetUrl(image)"
      :alt="imageAlt"
      class="absolute inset-0 w-full h-full object-cover"
    />
    <div v-else class="absolute inset-0"
         style="background: linear-gradient(160deg, #0c3b7a 0%, #041d45 100%);"></div>

    <!-- Gradient overlay: solid navy left → transparent right -->
    <div class="absolute inset-0"
         style="background: linear-gradient(to right, #041d45 0%, #041d45 42%, rgba(4,29,69,0.55) 68%, transparent 100%);"></div>

    <!-- Content: sits above overlays -->
    <div class="relative h-full flex flex-col px-12 pt-10 pb-14" style="width: 58%;">

      <!-- Sky accent bar -->
      <div class="mb-8 h-[3px] w-14 rounded-full"
           style="background: linear-gradient(90deg, #38bdf8, #0369a1);"></div>

      <!-- Title content (slot) -->
      <div class="flex-1 flex flex-col justify-center">
        <slot />
      </div>

      <!-- Presenter block -->
      <div v-if="presenter || role || institution"
           class="presenter-block pt-5"
           style="border-top: 1px solid rgba(255,255,255,0.15);">
        <div v-if="presenter" class="presenter-name">{{ presenter }}</div>
        <div v-if="role" class="presenter-meta">{{ role }}</div>
        <div v-if="institution" class="presenter-meta">{{ institution }}</div>
        <div v-if="date" class="presenter-date">{{ date }}</div>
      </div>
    </div>

  </div>
</template>
