<script lang="ts" setup>
import { DateTime } from "luxon";
import type { TimelinePost } from "../posts";
import PostWriter from "../components/PostWriter.vue";

const post: TimelinePost = {
  id: "-1",
  title: "Title",
  created: DateTime.now(),
};
</script>

<template>
  New Post
  <PostWriter :post="post" />
</template>
