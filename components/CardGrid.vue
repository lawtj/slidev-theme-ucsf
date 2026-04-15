<!--
  CardGrid — color-coded card layout with per-card v-click reveals.

  Usage:
    <CardGrid :items="[
      { title: 'Compressions', body: '→ forward flow', color: 'green' },
      { title: 'Defibrillation', body: '→ electrical reset', color: 'amber' },
      { title: 'Epinephrine', body: '→ vasoconstriction for CPP', color: 'purple' },
      { title: 'Ventilation', body: '→ oxygen in, pressure balance', color: 'sky' },
    ]" />

    Three columns:
    <CardGrid :items="[...]" cols="3" />

  Props:
    items   — array of { title, body, color } objects (required)
    cols    — '2' | '3' | '4' (default: '2')

  Colors: red, amber, yellow, green, blue, sky, purple, gray

  Notes:
    Keep <v-click> explicit in the template. Rendering it indirectly via
    <component :is="..."> breaks Slidev click tracking and can cause all cards
    to appear at once.
-->

<script setup lang="ts">
import { Icon } from '@iconify/vue'

interface CardItem {
  title: string
  body?: string
  color?: string
  icon?: string
}

interface Props {
  items: CardItem[]
  cols?: '2' | '3' | '4'
}

const props = withDefaults(defineProps<Props>(), {
  cols: '2',
})

const colsClass: Record<string, string> = {
  '2': 'grid-cols-2',
  '3': 'grid-cols-3',
  '4': 'grid-cols-4',
}

// Color presets — bg, border, title text
const palette: Record<string, { bg: string; border: string; title: string; body: string }> = {
  red:    { bg: 'bg-red-50',    border: 'border-red-200',    title: 'text-red-700',    body: 'text-red-600' },
  amber:  { bg: 'bg-amber-50',  border: 'border-amber-200',  title: 'text-amber-700',  body: 'text-amber-600' },
  yellow: { bg: 'bg-yellow-50', border: 'border-yellow-200', title: 'text-yellow-700', body: 'text-yellow-600' },
  green:  { bg: 'bg-green-50',  border: 'border-green-200',  title: 'text-green-700',  body: 'text-green-600' },
  blue:   { bg: 'bg-blue-50',   border: 'border-blue-200',   title: 'text-blue-700',   body: 'text-blue-600' },
  sky:    { bg: 'bg-sky-50',    border: 'border-sky-200',    title: 'text-sky-700',    body: 'text-sky-600' },
  purple: { bg: 'bg-purple-50', border: 'border-purple-200', title: 'text-purple-700', body: 'text-purple-600' },
  gray:   { bg: 'bg-gray-50',   border: 'border-gray-200',   title: 'text-gray-700',   body: 'text-gray-600' },
}

function colors(color?: string) {
  return palette[color ?? 'gray'] ?? palette.gray
}
</script>

<template>
  <div class="grid gap-6 mt-8" :class="colsClass[cols]">
    <template v-for="(item, i) in items" :key="i">
      <v-click>
        <div
          class="border rounded-lg p-4 text-center"
          :class="[colors(item.color).bg, colors(item.color).border]"
        >
          <Icon v-if="item.icon" :icon="item.icon" class="text-3xl mx-auto mb-2" :class="colors(item.color).title" />
          <div class="font-bold text-lg" :class="colors(item.color).title">
            {{ item.title }}
          </div>
          <div v-if="item.body" class="text-base mt-1" :class="colors(item.color).body">
            {{ item.body }}
          </div>
        </div>
      </v-click>
    </template>
  </div>
</template>
