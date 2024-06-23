<template>
  <section>
    <ul>
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
    imageUrl: 'https://cataas.com/cat',
    title: 'This is a placeholder cat',
    about:
      'Using cataas.com, Im able to serve up random cat pictures in place of actual project content while developing the site',
    links: ['https://cataas.com/cat']
  }
])
</script>

<style scoped></style>
