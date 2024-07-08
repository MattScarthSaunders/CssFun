<template>
  <div class="detail" @click="$emit('zoomDetail')">
    <h6>{{ title }}</h6>
    <p>{{ body }}</p>
  </div>
</template>

<script setup lang="ts">
defineProps<{ title: string; body: string }>()
</script>

<style scoped>
.detail {
  display: flex;
  flex-direction: column;
  gap: 5px;
  width: 30%;
  height: 90%;
  background: white;
  overflow: hidden;
  border-left: 4px solid rgb(114, 84, 56);
  border-top: 4px solid rgb(114, 84, 56);
  border-right: 4px solid rgb(175, 124, 76);
  border-bottom: 4px solid rgb(175, 124, 76);
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.78);
  border-radius: 2px;
  padding: 20px;
}

.detail h6 {
  font-size: 2rem;
}
</style>
