<script setup lang="ts">
import { usePosts } from "../stores/posts";
import TimelineItem from "./TimelineItem.vue";
import { periods, Period } from "../constants";

const postsStore = usePosts();

await postsStore.fetchPosts();
</script>

<template>
  <nav class="is-primary panel">
    <span class="panel-tabs">
      <a
        :class="{ 'is-active': period === postsStore.selectedPeriod }"
        v-for="(period, index) of periods"
        :key="`${index} '+' ${period}`"
        @click="postsStore.setSelectedPeriod(period)"
      >
        {{ period }}
      </a>
    </span>

    <TimelineItem
      v-for="post in postsStore.filteredPosts"
      :key="post.id"
      :post="post"
    />
  </nav>
</template>

<style scoped></style>
