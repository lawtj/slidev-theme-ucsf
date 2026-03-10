<script setup lang="ts">
interface Props {
  title?: string
  leftHeader?: string
  rightHeader?: string
  section?: string
}

const props = withDefaults(defineProps<Props>(), {
  title: '',
  leftHeader: '',
  rightHeader: '',
  section: ''
})
</script>

<template>
  <div class="slidev-layout flex flex-col h-full">
    <!-- Title -->
    <h1 class="text-center font-black text-4xl leading-tight px-8 pt-6 pb-2">
      {{ title }}
    </h1>

    <!-- Image area -->
    <div class="flex-1 flex items-center justify-center overflow-hidden px-8">
      <slot name="image" />
    </div>

    <!-- Two-column text -->
    <div class="grid grid-cols-2 gap-8 px-8 pb-6">
      <div>
        <p v-if="leftHeader" class="font-bold text-base mb-1">{{ leftHeader }}</p>
        <slot name="left" />
      </div>
      <div>
        <p v-if="rightHeader" class="font-bold text-base mb-1">{{ rightHeader }}</p>
        <slot name="right" />
      </div>
    </div>

    <Footer :section="section" />
  </div>
</template>
