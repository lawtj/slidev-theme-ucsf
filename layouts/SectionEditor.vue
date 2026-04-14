
<template>
  <div
    class="absolute 
    left-0 
    top-50 
    w-4/5 h-25 rounded-xl shadow-lg p-8 flex flex-col justify-center items-start bg-gradient-to-r from-cyan-300 to-blue-900
    
    "
  >
  <div class="text-3xl font-bold">
    <slot name="title"/>
  </div>
  <div class="text-xl">
    <slot name="subtitle"/>
  </div>

</div>
</template>

<script setup>
// No props for now, but can be extended
</script>
