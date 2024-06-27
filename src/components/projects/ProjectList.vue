<template>
  <section ref="frameContainer" class="container">
    <dialog v-if="modalUrl !== ''" class="modal">
      <button class="close" @click="() => (modalUrl = '')">&times;</button>
      <iframe class="modalFrame" :src="modalUrl"></iframe>
    </dialog>
    <ul class="list">
      <ProjectItem
        v-bind:key="index"
        v-for="(project, index) in projects"
        :project="project"
        @modalUrlUpdate="
          (url: string) => {
            modalUrl = url
          }
        "
      />
    </ul>
  </section>
</template>

<script setup lang="ts">
import { ref, watchEffect, type Ref } from 'vue'
import ProjectItem from './ProjectItem.vue'
import type { Project } from './types'

const modalUrl = ref('')

const projects = ref<Project[]>([
  {
    imageUrl: 'https://synthwaveryder.netlify.app',
    title: 'SynthwaveRyder',
    isInteractive: true,
    detail: {
      title: 'Synthwave Ryder',
      body: "A project in which I taught myself about perspective animation using css. I'm a synthwave music fan and decided it might be fun to make a themed wrapper for a playlist, imposing the limitation of no javascript."
    }
  },
  {
    imageUrl: 'src/frames/solaris/solaris.html',
    title: 'solaris',
    isInteractive: false,
    detail: {
      title: 'Solaris',
      body: 'This was done as a team code-challenge in which we attempted to replicate the retro Solaris movie poster within a 1-hour timeframe, using html, css and javascript.'
    }
  }
])

function rescale(frame: HTMLElement | undefined, scale: Ref<number>) {
  if (frame) {
    scale.value = frame.clientWidth / 1920
  }
}

const frameContainer = ref<HTMLElement | undefined>()
const scale = ref(1)

watchEffect(() => {
  rescale(frameContainer.value, scale)

  window.addEventListener('resize', () => {
    rescale(frameContainer.value, scale)
  })
})
</script>

<style scoped>
.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.list {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 200px;
}

.modal {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.562);
  z-index: 99;
}

.modalFrame {
  width: 1920px;
  height: 1080px;
  zoom: 1;
  transform: scale(v-bind(scale - 0.2));
  -ms-zoom: 1;
  -moz-transform: scale(v-bind(scale - 0.2));
  -o-transform: scale(v-bind(scale - 0.2));
  -webkit-transform: scale(v-bind(scale - 0.2));
  border: none;
}
.close {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 20px;
  height: 20px;
  background: white;
  border: none;
  border-radius: 100%;
}
</style>
