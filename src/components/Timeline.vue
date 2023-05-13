<script setup lang="ts">
import { ref } from 'vue'

const periods = ['Today', 'This Week', 'This Month']

const selectedPeriod = ref('Today')

const selectPeriod = (period: string) => {
  console.log(period)
  selectedPeriod.value = period
}
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
  </nav>
</template>

<style scoped>
</style>