<template>
  <li class="project">
    <div ref="frame" class="frameContainer">
      <div v-if="!project.isInteractive" class="overlay"></div>
      <iframe :id="project.title + `frame`" class="frame" :src="project.imageUrl" />
    </div>
    <h2 class="title">{{ project.title }}</h2>
  </li>
</template>

<script setup lang="ts">
import { ref, watchEffect } from 'vue'
import type { Project } from './types'

defineProps<{ project: Project }>()

const frame = ref<HTMLElement | undefined>()
const scale = ref(1)

watchEffect(() => {
  window.addEventListener('resize', () => {
    if (frame.value) {
      console.log(frame.value.clientWidth)
      console.log(frame.value.clientWidth / 1920)
      scale.value = frame.value.clientWidth / 1920
    }
  })
})
</script>

<style scoped>
.project {
  list-style-type: none;
  padding: 20px;
  border: 1px solid red;
  width: 30vw;
  max-height: 30vh;
}

.frameContainer {
  position: relative;
  width: 100%;
  overflow: hidden;
}

.title {
  font-size: 1.2rem;
}

.frame {
  width: 1920px;
  height: 1080px;
  border: 1px solid black;
  zoom: 1;
  transform: scale(v-bind(scale));
  transform-origin: 0 0;
  -ms-zoom: 1;
  -moz-transform: scale(v-bind(scale));
  -moz-transform-origin: 0 0;
  -o-transform: scale(v-bind(scale));
  -o-transform-origin: 0 0;
  -webkit-transform: scale(v-bind(scale));
  -webkit-transform-origin: 0 0;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
}

.overlay:hover {
  cursor: pointer;
}
</style>
