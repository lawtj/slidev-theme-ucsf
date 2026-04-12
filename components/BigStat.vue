<!--
  BigStat — large number or phrase with a subtitle.

  Usage:
    <BigStat value="1 in 4" label="In-hospital cardiac arrest survival to discharge" />

    <BigStat value="79 cpm" label="Average compression rate in non-survivors"
             valueClass="text-red-500" />

  Props:
    value      — the hero number or phrase (required)
    label      — subtitle text below the value (optional)
    valueClass — extra classes on the value, e.g. color (default: '')
-->

<script setup lang="ts">
interface Props {
  value: string
  label?: string
  valueClass?: string
}

withDefaults(defineProps<Props>(), {
  label: '',
  valueClass: '',
})
</script>

<template>
  <div class="flex flex-col items-center justify-center text-center gap-4">
    <div class="text-7xl font-black leading-tight" :class="valueClass">
      {{ value }}
    </div>
    <div v-if="label" class="text-lg text-gray-400 max-w-md">
      {{ label }}
    </div>
  </div>
</template>
