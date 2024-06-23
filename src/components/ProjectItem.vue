<template>
  <li>
    <img class="image" :src="project.imageUrl" />
    <h2 class="title">{{ project.title }}</h2>
    <p class="about">{{ project.about }}</p>
    <ul class="links">
      <a v-bind:key="index" v-for="(link, index) in project.links" :src="link"></a>
    </ul>
  </li>
</template>

<script setup lang="ts">
import type { Project } from './types'

defineProps<{ project: Project }>()
</script>

<style scoped></style>
