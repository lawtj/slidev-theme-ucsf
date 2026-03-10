<script setup lang="ts">
import Card from '../components/Card.vue'

interface Props {
  leftHeader?: string
  rightHeader?: string
  gap?: string
  section?: string
}

const props = withDefaults(defineProps<Props>(), {
  leftHeader: '',
  rightHeader: '',
  gap: 'gap-4',
  section: ''
})
</script>

<template>
  <div class="slidev-layout ">
    <div :class="['grid grid-cols-2 w-full flex-1', gap]">
      <Card :header="leftHeader" width="w-full">
        <slot name="left" />
      </Card>
      <Card :header="rightHeader" width="w-full">
        <slot name="right" />
      </Card>
    </div>
    <Footer :section="section" />
  </div>
</template>
