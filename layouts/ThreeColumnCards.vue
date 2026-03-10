<script setup lang="ts">
import Card from '../components/Card.vue'

interface Props {
  leftHeader?: string
  centerHeader?: string
  rightHeader?: string
  gap?: string
}

const props = withDefaults(defineProps<Props>(), {
  leftHeader: '',
  centerHeader: '',
  rightHeader: '',
  gap: 'gap-4'
})
</script>

<template>
  <div class="slidev-layout">
    <div :class="['grid grid-cols-3 gap-6']">
      <Card :header="leftHeader" >
        <slot name="left" />
      </Card>
      <Card :header="centerHeader">
        <slot name="center" />
      </Card>
      <Card :header="rightHeader">
        <slot name="right" />
      </Card>
    </div>
</div>
</template>
