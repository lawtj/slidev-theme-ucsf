<script setup lang="ts">
import { withBase } from 'vite'

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
  <div class="slidev-layout contrast-image-right h-full flex overflow-hidden" style="background: #18232e;">
    <!-- Left: text content panel -->
    <div class="content-panel flex-1 flex flex-col justify-center px-10 py-8 pb-14 min-w-0">
      <slot />
    </div>

    <!-- Right: image fills edge-to-edge -->
    <div class="image-panel relative shrink-0" style="width: 54%;">
      <img
        v-if="image"
        :src="withBase(image)"
        :alt="imageAlt"
        :style="`object-position: ${imagePosition}`"
        class="absolute inset-0 w-full h-full object-cover"
      />
      <slot v-else name="image" />
    </div>
  </div>
</template>
