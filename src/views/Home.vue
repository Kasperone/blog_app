<script setup lang="ts">
import Timeline from "../components/Timeline.vue";
</script>

<template>
  <Suspense>
    <template #default>
      <Timeline />
    </template>
    <template #fallback>Loading...</template>
  </Suspense>
</template>
