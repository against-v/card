<script setup lang="ts"></script>

<template>
  <div :class="$style.container">
    <div :class="$style.desk"></div>
  </div>
</template>

<style module>
.container {
  height: 100%;
  background-color: #000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
}
.desk {
  max-width: 620px;
  width: 100%;
  padding: 10px;
  background-color: #948e8e;
}
</style>
