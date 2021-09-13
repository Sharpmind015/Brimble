<template>
  <Dialog class="modal" :open="isOpen" @close="setIsOpen">
    <DialogOverlay />

    <DialogTitle class="visuallyHidden">Status message</DialogTitle>
    <DialogDescription class="visuallyHidden">
      {{response.status}}
    </DialogDescription>

    <div class="modal-tick">
      <svg width="60" height="38" viewBox="0 0 60 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect class="h-0 rect-1" width="4.83068" rx="2.41534" transform="matrix(-0.855371 0.518015 -0.495837 -0.868415 16.1709 35.8726)" fill="white"/>
        <rect class="h-0 rect-2" width="4.72217" rx="2.36109" transform="matrix(0.569354 0.822092 -0.806982 0.590575 57.4912 0)" fill="white"/>
      </svg>
    </div>
    <h4 class="modal-status">Completed!
      <div class="modal-status-line modal-status-line-1"></div>
      <div class="modal-status-line modal-status-line-2"></div>
    </h4>
    <p v-if="response.status = 'Yay, we did it!!'" class="modal-message mb-9">You are now number <span class="modal-number">{{response.data.number}}</span> on the waiting list</p>
    <p class="modal-message">We will keep you updated</p>
    <button class="modal-cancel" aria-label="Click button to close modal" @click="setIsOpen(false)">
      <svg width="38" height="38" viewBox="0 0 38 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M19.0016 19.0001L27.303 27.3016M10.7002 27.3016L19.0016 19.0001L10.7002 27.3016ZM27.303 10.6987L19 19.0001L27.303 10.6987ZM19 19.0001L10.7002 10.6987L19 19.0001Z" stroke="#BDBDBD" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </button>
  </Dialog>
</template>

<script>
  import { ref } from "vue";
  import {
    Dialog,
    DialogOverlay,
    DialogTitle,
    DialogDescription,
  } from "@headlessui/vue";

  export default {
    name: 'Modal',
    components: { Dialog, DialogOverlay, DialogTitle, DialogDescription },
    setup() {
      let isOpen = ref(true);

      return {
        isOpen,
        setIsOpen(value) {
          isOpen.value = value;
        }
      };
    },
    props: ['response']
  };
</script>