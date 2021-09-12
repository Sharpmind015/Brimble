<script>
import {gsap} from 'gsap'

export default {
  name: 'Modal',
  mounted() {
    gsap.timeline()
    .to('.modal', {top: '50%', duration: 1, ease: 'Expo.in'})
    .to('.modal-status-line', {width: '125px',stagger: 0.2, ease: 'Expo.in'})
    .to('.rect-1', {width: '4.83068px', ease: 'Expo.out'})
    .to('.rect-2', {width: '4.72217px', ease: 'Expo.out'})
  }
  // props: ['item', 'toggle']
}
</script>

<template>
  <section class="modal" role="dialog">
    <div class="modal-tick">
      <svg width="60" height="38" viewBox="0 0 60 38" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect class="w-0 rect-1" height="24.2795" rx="2.41534" transform="matrix(-0.855371 0.518015 -0.495837 -0.868415 16.1709 35.8726)" fill="white"/>
        <rect class="w-0 rect-2" height="58.0323" rx="2.36109" transform="matrix(0.569354 0.822092 -0.806982 0.590575 57.4912 0)" fill="white"/>
      </svg>
    </div>
    <h4 class="modal-status">Completed!
      <div class="modal-status-line modal-status-line-1"></div>
      <div class="modal-status-line modal-status-line-2"></div>
    </h4>
    <p class="modal-message mb-9">You are now number <span class="modal-number">321</span> on the waiting list</p>
    <p class="modal-message">We will keep you updated</p>
    <svg class="modal-cancel" width="38" height="38" viewBox="0 0 38 38" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M19.0016 19.0001L27.303 27.3016M10.7002 27.3016L19.0016 19.0001L10.7002 27.3016ZM27.303 10.6987L19 19.0001L27.303 10.6987ZM19 19.0001L10.7002 10.6987L19 19.0001Z" stroke="#BDBDBD" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
  </section>
</template>

