<script setup lang="ts">


</script>

<template>
  <div class="slidev-layout">
    <div :class="['grid grid-cols-3 gap-6']">
      <slot name="left" />
      <slot name="center" />
        <slot name="right" />
    </div>
</div>
</template>
