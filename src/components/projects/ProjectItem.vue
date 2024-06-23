<template>
  <li class="project">
    <img class="image" :src="project.imageUrl" />
    <h2 class="title">{{ project.title }}</h2>
    <p class="about">{{ project.about }}</p>
    <ProjectLinksList :links="project.links"></ProjectLinksList>
  </li>
</template>

<script setup lang="ts">
import ProjectLinksList from './ProjectLinksList.vue'
import type { Project } from './types'

defineProps<{ project: Project }>()
</script>

<style scoped>
.project {
  list-style-type: none;
}

.image {
  width: 50%;
  height: 50%;
}
</style>
