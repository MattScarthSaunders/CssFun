<template>
  <main>
    <ProjectList></ProjectList>
  </main>
</template>

<script setup lang="ts">
import ProjectList from './components/projects/ProjectList.vue'
</script>

<style scoped>
main {
  width: 100vw;
  height: 100vh;
  background-color: rgb(38, 38, 38);
  overflow: hidden;
}
</style>
