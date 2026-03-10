<script setup lang="ts">
import { resolveAssetUrl } from '@slidev/client/layoutHelper.ts'

interface Props {
  image?: string
  imageAlt?: string
  imagePosition?: string
}

const props = withDefaults(defineProps<Props>(), {
  image: '',
  imageAlt: 'Slide image',
  imagePosition: 'center',
})
</script>

<template>
  <div class="slidev-layout statement-image-columns h-full overflow-hidden"
       style="display: grid; grid-template-rows: auto 1fr 38%;">
    <!-- Bold centered title -->
    <div class="title-area text-center px-10 pt-6 pb-1">
      <slot />
    </div>

    <!-- Centered contained image -->
    <div class="image-area flex items-center justify-center overflow-hidden px-8 py-2">
      <img
        v-if="image"
        :src="resolveAssetUrl(image)"
        :alt="imageAlt"
        :style="`object-position: ${imagePosition}`"
        class="max-w-full max-h-full object-contain"
      />
      <slot v-else name="image" />
    </div>

    <!-- Two text columns -->
    <div class="columns-area grid grid-cols-2 gap-8 px-10 pb-12">
      <div class="col-left">
        <slot name="left" />
      </div>
      <div class="col-right">
        <slot name="right" />
      </div>
    </div>
  </div>
</template>
