<script setup lang="ts">
import { ref ,computed } from 'vue'
import { TimelinePost, today, thisWeek, thisMonth } from "../posts";
import { DateTime } from "luxon";
import { usePosts } from "../stores/posts";
import TimelineItem from "./TimelineItem.vue";

const postStore = usePosts()

const periods = ['Today', 'This Week', 'This Month'] as const
type Period = typeof periods[number]

const selectedPeriod = ref<Period>('Today')

const selectPeriod = (period: Period) => {
  selectedPeriod.value = period
}

const posts = computed<TimelinePost[]>(() => {
  return postStore.ids.map(id => {
    const post = postStore.all.get(id)

    if(!post) {
      throw Error(`Post with id of ${id} was expected but not found.`)
    }

    return {...post, created: DateTime.fromISO(post.created)}
  }).filter(post => {

    if (selectedPeriod.value === 'Today') {
      return post.created >= DateTime.now().minus({day: 1})
    }

    if (selectedPeriod.value === 'This Week') {
      return post.created >= DateTime.now().minus({week: 1})
    }

    return post
  })
})

</script>

<template>
  <nav  class="is-primary panel">
    {{ selectedPeriod }}
    <span class="panel-tabs">
      <a :class="{ 'is-active': period === selectedPeriod }"
         v-for="(period, index) of periods"
         :key="`${index} '+' ${period}`"
         @click="selectPeriod(period)">
        {{ period }}
      </a>
    </span>

    <TimelineItem
       v-for="post in posts"
       :key="post.id"
       :post="post"
    />
  </nav>
</template>

<style scoped>
</style>