<template>
  <main>
    <HeaderCustom></HeaderCustom>
    <ProjectList></ProjectList>
  </main>
</template>

<script setup lang="ts">
import HeaderCustom from './components/HeaderCustom.vue'
import ProjectList from './components/projects/ProjectList.vue'
</script>

<style scoped>
main {
  height: 100vh;
}
</style>
