<script setup lang="ts">
import TheCards from "@/components/TheCards/TheCards.vue";
</script>

<template>
  <main :class="$style.container">
    <TheCards />
  </main>
</template>

<style module>
.container {
  height: 100%;
}
</style>
