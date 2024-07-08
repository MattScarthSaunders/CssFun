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
  width: 10%;
  height: 30%;
  background: white;
  position: absolute;
  right: -100px;
  top: 37.5%;
  font-size: 0.5rem;
  padding: 5px;
  overflow: hidden;
  border-left: 4px solid rgb(114, 84, 56);
  border-top: 4px solid rgb(114, 84, 56);
  border-right: 4px solid rgb(175, 124, 76);
  border-bottom: 4px solid rgb(175, 124, 76);
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.78);
  border-radius: 2px;
}

.detail:hover {
  cursor: pointer;
  filter: brightness(1.2);
}

.detail h6,
p {
  text-overflow: ellipsis;
  filter: blur(1px) brightness(0.9);
}

.detail p {
  font-size: 0.25rem;
}
</style>
