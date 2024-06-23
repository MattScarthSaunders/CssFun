<template>
  <ul class="links">
    <li class="linkItem">
      <a class="link" v-bind:key="index" v-for="(link, index) in links" :src="link">{{ link }}</a>
    </li>
  </ul>
</template>

<script setup lang="ts">
defineProps<{ links: string[] }>()
</script>

<style scoped>
.links {
  margin: 0;
  padding: 0;
}

.linkItem {
  list-style-type: none;
  padding: 0;
}
</style>
