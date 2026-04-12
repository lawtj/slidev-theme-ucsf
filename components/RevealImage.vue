<!--
  RevealImage — progressively reveal or cover regions of an image using slide clicks.

  REQUIRED: add `clicks: N` to the slide frontmatter, where N is the number
  of click steps the slide needs (one per cover transition).

  Usage:
    <RevealImage
      src="/assets/image.png"
      imgClass="h-full w-auto"
      :covers="[
        { side: 'bottom', size: '50%', to: 0 },
        { side: 'right',  size: '33%', from: 2, to: 3 },
      ]"
    />

  Props:
    src        — image path
    height     — max height as % of slide or px e.g. "85%", "400px". Percentages are
                 resolved against the 552px slide canvas so they work in all layouts.
    imgClass   — override image classes if needed (rarely necessary)
    covers     — array of Cover objects (see below)

  Cover options:
    side   — which edge to cover: 'top' | 'bottom' | 'left' | 'right'
    size   — how much to cover, as a CSS value e.g. '50%', '33%'  (default: '50%')
    color  — cover color (default: 'white')
    from   — first click number where this cover is visible          (default: 0)
    to     — last click number where it stays visible; omit = forever

  Lines:
    SVG lines overlaid on the image. Coordinates are percentages of the image size.

    <RevealImage
      src="/assets/image.png"
      imgClass="h-full w-auto"
      :lines="[
        { x1: '0%', y1: '50%', x2: '100%', y2: '50%', from: 1 },
        { x1: '25%', y1: '0%', x2: '25%', y2: '100%', stroke: '#ff0000', strokeWidth: 3, to: 2 },
      ]"
    />

  Line options:
    Shorthand (recommended):
      h       — horizontal line at this y position e.g. h: '50%'
      v       — vertical line at this x position   e.g. v: '25%'
      start   — where the line begins (default: '0%')
      end     — where the line ends   (default: '100%')

    Explicit (full control):
      x1, y1, x2, y2 — start/end points as percentage strings

    stroke      — line color (default: '#ef4444' red)
    strokeWidth — px thickness  (default: 2)
    from, to    — same click visibility logic as covers

  Recipes:
    v-click.hide equivalent (visible at 0, gone at click 1):  { to: 0 }
    v-click equivalent (hidden at 0, appears at click 1):      { from: 1 }
    appears then disappears (click 2 → click 4):               { from: 2, to: 3 }
-->

<script setup lang="ts">
import { computed } from 'vue'
import { useNav } from '@slidev/client'
import { resolveAssetUrl } from '@slidev/client/layoutHelper.ts'

const SLIDE_HEIGHT = 552 // Slidev default 16:9 canvas height in px

type Side = 'top' | 'bottom' | 'left' | 'right'

interface Cover {
  side: Side
  size?: string   // CSS size value e.g. '50%', '33%' — defaults to '50%'
  color?: string  // defaults to white
  from?: number   // first click where this cover is visible — defaults to 0
  to?: number     // last click where it stays visible — omit to stay forever
}

interface Line {
  // Shorthand
  h?: string      // horizontal line at y position e.g. '50%'
  v?: string      // vertical line at x position   e.g. '25%'
  start?: string  // span start (default '0%')
  end?: string    // span end   (default '100%')
  // Explicit
  x1?: string
  y1?: string
  x2?: string
  y2?: string
  stroke?: string       // defaults to '#ef4444'
  strokeWidth?: number  // defaults to 2
  from?: number
  to?: number
}

interface Props {
  src: string
  alt?: string
  covers?: Cover[]
  lines?: Line[]
  imgClass?: string
  height?: string  // e.g. '85%', '400px' — resolved to px and applied as max-height on img
}

const props = withDefaults(defineProps<Props>(), {
  alt: '',
  covers: () => [],
  lines: () => [],
  imgClass: 'w-auto',
  height: '',
})

const { clicks } = useNav()

// Convert height to px so it works in all layouts (including center, which
// has an auto-height inner wrapper that breaks percentage resolution).
const resolvedMaxHeight = computed(() => {
  if (!props.height) return undefined
  if (props.height.endsWith('%'))
    return `${(parseFloat(props.height) / 100) * SLIDE_HEIGHT}px`
  return props.height
})

function isVisible(cover: Cover): boolean {
  return clicks.value >= (cover.from ?? 0) && clicks.value <= (cover.to ?? Infinity)
}

function resolveLineCoords(line: Line) {
  const start = line.start ?? '0%'
  const end   = line.end   ?? '100%'
  if (line.h !== undefined)
    return { x1: start, y1: line.h, x2: end, y2: line.h }
  if (line.v !== undefined)
    return { x1: line.v, y1: start, x2: line.v, y2: end }
  return { x1: line.x1 ?? '0%', y1: line.y1 ?? '0%', x2: line.x2 ?? '100%', y2: line.y2 ?? '100%' }
}

function coverStyle(cover: Cover): Record<string, string> {
  const size = cover.size ?? '50%'
  const color = cover.color ?? 'white'
  const base: Record<string, string> = { background: color }

  if (cover.side === 'top')    return { ...base, top: '0', left: '0', right: '0', height: size }
  if (cover.side === 'bottom') return { ...base, bottom: '0', left: '0', right: '0', height: size }
  if (cover.side === 'left')   return { ...base, top: '0', bottom: '0', left: '0', width: size }
  if (cover.side === 'right')  return { ...base, top: '0', bottom: '0', right: '0', width: size }
  return base
}
</script>

<template>
  <div class="relative" style="width: fit-content;">
    <img
      :src="resolveAssetUrl(src)"
      :alt="alt"
      :class="imgClass"
      :style="resolvedMaxHeight ? { maxHeight: resolvedMaxHeight } : {}"
      class="block"
    />

    <!-- Cover divs -->
    <div
      v-for="(cover, i) in covers"
      :key="`cover-${i}`"
      v-show="isVisible(cover)"
      class="absolute"
      :style="coverStyle(cover)"
    />

    <!-- SVG line overlay -->
    <svg
      v-if="lines.length"
      class="absolute inset-0 w-full h-full pointer-events-none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <line
        v-for="(line, i) in lines"
        :key="`line-${i}`"
        v-show="isVisible(line)"
        v-bind="resolveLineCoords(line)"
        :stroke="line.stroke ?? '#ef4444'"
        :stroke-width="line.strokeWidth ?? 2"
        stroke-linecap="round"
      />
    </svg>
  </div>
</template>
