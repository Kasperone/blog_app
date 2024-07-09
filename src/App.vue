<script setup lang="ts">
import Timeline from "./components/Timeline.vue";
</script>

<template>
  <div class="section">
    <div class="container">
      <Suspense>
        <template #default>
          <Timeline />
        </template>
        <template #fallback>Loading...</template>
      </Suspense>
    </div>
  </div>
</template>

<style scoped>
@import "https://cdn.jsdelivr.net/npm/bulma@0.9.4/css/bulma.min.css";
</style>
