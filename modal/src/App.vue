<script setup>

import { ref } from 'vue'
import { onClickOutside } from '@vueuse/core'

const isOpen = ref(false) 
const modal = ref(null)

onClickOutside(modal, () => (isOpen.value = false))
</script>

<template>
  <div class="container">
    <h1>
      Vue modal
    </h1>
    <button @click="isOpen = true">
      open the modal
    </button>
    <Teleport to="#modal">
      <Transition name="modal">
      <div class="modal-bg" v-if="isOpen" >
          <div class="modal" ref="modal">
            <p>
              Click outside this modal to close it.
            </p>
            <button @click="isOpen = false">
              close the fucking modal
            </button>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<style>
.modal-bg {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  background-color: rgba(0, 0, 0, 0.5) ;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  position: relative ;
  background: white; 
  padding: 50px 100px;
  border-radius: 5px;
  box-shadow: 0px 10px 5px 2px rgba(0, 0, 0, 0.1);
  display: flex;
}
.modal-enter-active,
.modal-leave-active {
  transition: all 0.25s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.1);
}

.container {
  background-color: white ;
  display: flex; 
  flex-direction: column;
  align-items:center;
  justify-content: center;
}
body {
  margin: 0;
  padding: 0;
}
</style>
