<template>
  <li ref="frame" class="project">
    <div class="lamp"></div>
    <iframe :id="project.title + `frame`" class="frame" :src="project.imageUrl"></iframe>
    <iframe :id="project.title + `frameBlur`" class="frameBlur" :src="project.imageUrl"></iframe>
    <div class="controls">
      <button class="zoom" @click="$emit('modalUrlUpdate', project.imageUrl)">
        {{ zoom }}
      </button>
    </div>
    <div class="detail">
      <h6>{{ project.detail.title }}</h6>
      <p>{{ project.detail.body }}</p>
    </div>
  </li>
</template>

<script setup lang="ts">
import { ref, watchEffect, type Ref } from 'vue'
import type { Project } from './types'

defineProps<{ project: Project }>()

const frame = ref<HTMLElement | undefined>()
const scale = ref(1)
const zoom = ref('+')

function rescale(frame: HTMLElement | undefined, scale: Ref<number>) {
  if (frame) {
    scale.value = frame.clientWidth / 1920
  }
}

watchEffect(() => {
  rescale(frame.value, scale)

  window.addEventListener('resize', () => {
    rescale(frame.value, scale)
  })
})
</script>

<style scoped>
.project {
  position: relative;
  list-style-type: none;
  width: 30vw;
  height: 30vh;
}

.controls {
  position: absolute;
  bottom: -80px;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.zoom {
  position: relative;
  font-size: 1rem;
  width: 50px;
  height: 25px;
  border: none;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 3px;
  background: none;
  border: 2px solid white;
  color: white;
  cursor: pointer;
}

.zoom:active {
  background: rgba(0, 0, 0, 0.201);
  color: rgba(255, 255, 255, 0.829);
  box-shadow: inset 0 0 5px black;
}

.frame {
  border-radius: 15px;
  border: 1px solid black;
  position: absolute;
  width: 1920px;
  height: 1080px;
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
  z-index: 1;
}

.frameBlur {
  top: -2%;
  left: -2%;
  z-index: 0;
  position: absolute;
  width: 1920px;
  height: 1080px;
  filter: blur(100px);
  zoom: 1;
  transform: scale(v-bind(scale + 0.02));
  transform-origin: 0 0;
  -ms-zoom: 1;
  -moz-transform: scale(v-bind(scale + 0.02));
  -moz-transform-origin: 0 0;
  -o-transform: scale(v-bind(scale + 0.02));
  -o-transform-origin: 0 0;
  -webkit-transform: scale(v-bind(scale + 0.02));
  -webkit-transform-origin: 0 0;
  pointer-events: none;
}
.lamp {
  position: absolute;
  z-index: 2;
  width: 10%;
  height: 7.5%;
  background-color: rgb(0, 53, 4);
  top: -15%;
  left: 45%;
  box-shadow:
    0 75px 50px white,
    inset 2px 5px 5px rgb(2, 23, 0),
    0 -20px 50px black,
    inset -5px 5px 15px -10px rgb(29, 206, 2);
  border-radius: 15px 15px 0 0;
  border-bottom: 1px solid burlywood;
}

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
