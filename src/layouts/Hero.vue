<script>
import Heading from "../components/Heading.vue"
import Modal from "../components/Modal.vue"
import {gsap} from 'gsap'

export default {
  name: "Hero",
  components: {
    Heading,
    Modal
  },
  data() {
    return {
      tools: [
        {
          name: "vue",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510746/vue_ml7atz.svg",
        },
        {
          name: "ember",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510817/ember_xjetmd.svg",
        },
        {
          name: "react",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510883/react_knhn9b.svg",
        },
        {
          name: "nuxt",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510913/nuxt_egzrba.svg",
        },
        {
          name: "gatsby",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510941/gatsby_xkzjth.svg",
        },
        {
          name: "svelte",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631510975/svelte_xwiupt.svg",
        },
        {
          name: "angular",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511025/angular_lkh7fl.svg",
        },
        {
          name: "next",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511058/next_vjvp3a.svg",
        },
        {
          name: "javascript",
          src: "https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511086/javascript_djuubq.svg",
        },
      ],
      showModal: false,
      response: {
        status: '',
        data: {
          number: ''
        }
      }
    };
  },
  emits: ['toggle'],
  mounted() {
    gsap.fromTo(`.tool-anim`, {scale: 0, rotate: 260}, {scale: 1, rotate: 0, stagger: 0.2, ease: "Bounce.out"})
    window.modalTl = gsap.timeline({pause: true});
    modalTl
    .to('.modal', {top: '50%', duration: 1, ease: 'Expo.in'})
    .to('.modal-status-line', {width: '125px',stagger: 0.2, ease: 'Expo.in'})
    .to('.rect-1', {height: '24.2795px', ease: 'Expo.out'})
    .to('.rect-2', {height: '58.0323px', ease: 'Expo.out'})
    modalTl.reverse() 
  },
  props: ['isToggle'],
  methods: {
    handleSubmit() {
      //API test :)
      this.response = {
        status: 'Yay, we did it!!',
        data: {
          number: 666,
        }
      }
      //response ? 'Show animation' : 'return or error modal, whatever floats your boat :)' 
      if(!this.showModal) {
        modalTl.play();
        this.showModal = !this.showModal;
      }
    },
    closeModal() {
        modalTl.reverse();
        this.showModal = !this.showModal;
    }
  }
};
</script>

<template>
  <section class="hero">
    <div class="tools">
      <img
        :class="`absolute ${tool.name} hidden xl:block tool-anim`"
        :src="tool.src"
        alt=""
        :key="index"
        v-for="(tool, index) in tools"
      />
    </div>
    <Heading :toggle="isToggle" />
    <p class="info">Be the first to know when BRIMBLE launches</p>
    <form @submit.prevent="handleSubmit" class="form">
      <label class="visuallyHidden" for="waitlist">
        Input your email address
      </label>
      <input
        required
        placeholder="email address"
        class="input-mail"
        type="email"
        name="waitlist"
        id="waitlist"
      />
      <input class="form-btn" type="submit" value="Join Waitlist" />
    </form>
    <button v-on:click="$emit('toggle')" class="toggle-switch" role="switch">
      <span class="toggle-mode light-mode">Light mood</span>
      <span class="toggle-mode dark-mode">Dark mood</span>
      <div class="ellipse">
        <img v-if="isToggle === 'Dark'" src="https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511508/Dark_jeazqh.png" alt="">
        <img v-if="isToggle === 'Light'" src="https://res.cloudinary.com/dexg5uy3d/image/upload/v1631511590/Light_bzhsrd.png" alt="">
      </div>  
    </button>
    <Modal :response="response" @close="closeModal" />
    <div @click="closeModal" v-if="showModal" class="overlay"></div> 
  </section>
</template>
