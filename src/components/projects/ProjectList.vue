<template>
  <section ref="frameContainer" class="container">
    <ProjectRenderModal v-if="modalUrl !== ''" @close="updateUrl">
      <iframe class="modalFrame" :src="modalUrl"></iframe>
    </ProjectRenderModal>
    <ProjectRenderModal v-if="modalTitle !== ''" @close="updateTitle">
      <ProjectDetailMacro
        class="overrideDetail"
        :title="zoomedProject?.detail.title!"
        :body="zoomedProject?.detail.body!"
      ></ProjectDetailMacro>
    </ProjectRenderModal>

    <ul class="list">
      <ProjectItem
        v-bind:key="index"
        v-for="(project, index) in projects"
        :project="project"
        @modalUrlUpdate="updateUrl"
        @zoomDetail="updateTitle"
      />
    </ul>
  </section>
</template>

<script setup lang="ts">
import { computed, ref, watchEffect, type Ref } from 'vue'
import type { Project } from './types'
import ProjectItem from './ProjectItem.vue'
import ProjectDetailMacro from './ProjectDetailMacro.vue'
import ProjectRenderModal from './ProjectRenderModal.vue'

const modalUrl = ref('')
const modalTitle = ref('')
const zoomedProject = computed(() =>
  projects.value.find((p) => p.detail.title === modalTitle.value)
)

const updateUrl = (url: string) => {
  modalUrl.value = url
}
const updateTitle = (title: string) => {
  modalTitle.value = title
}

const projects = ref<Project[]>([
  {
    imageUrl: 'https://synthwaveryder.netlify.app',
    isInteractive: true,
    detail: {
      title: 'Synthwave Ryder',
      body: "A project in which I taught myself about perspective animation using css. I'm a synthwave music fan and decided it might be fun to make a themed wrapper for a playlist, imposing the limitation of no javascript."
    }
  },
  {
    imageUrl: 'src/frames/solaris/solaris.html',
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
</style>
