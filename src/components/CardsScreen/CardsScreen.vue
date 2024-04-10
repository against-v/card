<script setup lang="ts">
import CssCards from "@/components/CssCards/CssCards.vue";
</script>

<template>
  <div :class="$style.container">
    <CssCards />
  </div>
</template>

<style module>
.container {
  height: 100%;
}
</style>
