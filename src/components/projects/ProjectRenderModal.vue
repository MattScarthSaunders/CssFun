<template>
  <dialog class="modal">
    <button class="close" @click="$emit('close', '')">&times;</button>
    <slot />
  </dialog>
</template>

<script setup lang="ts"></script>

<style scoped>
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
