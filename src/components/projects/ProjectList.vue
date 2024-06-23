<template>
  <section class="container">
    <ul class="list">
      <ProjectItem v-bind:key="index" v-for="(project, index) in projects" :project="project" />
    </ul>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import ProjectItem from './ProjectItem.vue'
import type { Project } from './types'

const projects = ref<Project[]>([
  {
    imageUrl: 'https://synthwaveryder.netlify.app',
    title: 'SynthwaveRyder',
    isInteractive: true
  },
  {
    imageUrl: 'https://cataas.com/cat',
    title: 'This is a placeholder cat',
    isInteractive: false
  },
  {
    imageUrl: 'https://cataas.com/cat',
    title: 'This is a placeholder cat',
    isInteractive: false
  }
])
</script>

<style scoped>
.container {
  padding: 20px;
}

.list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
</style>
