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

const projects = ref<Project[]>([{ imageUrl: '', title: 'test', about: 'test', links: ['test'] }])
</script>

<style scoped></style>
