<script
>
import Header from "./layouts/Header.vue";
import Hero from "./layouts/Hero.vue";
import {gsap} from 'gsap';

export default {
  name: 'App',
  components: {
    Header,
    Hero
  },
  data() {
    return {
      menu: [
        'Home', 'Pricing', 'About', 'Framework'
      ],
      isToggle: ''
    }
  },
  methods: {
    toggle: function() {
    if (localStorage.theme === 'Dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
        gsap.to('.ellipse', {x: '0'})
        document.documentElement.classList.remove('dark')
        this.isToggle = "Light"
        localStorage.theme = 'Light'
    } else {
        gsap.to('.ellipse', {x: '-200%'})
        document.documentElement.classList.add('dark')
        this.isToggle = "Dark"
        localStorage.theme = 'Dark'
    }
    }
  },
  mounted() {
    if (localStorage.theme === 'Dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
      gsap.to('.ellipse', {x: '-200%'})
      this.isToggle = "Dark"
      document.documentElement.classList.add('dark')
    } else {
        gsap.to('.ellipse', {x: '0'})
        this.isToggle = "Light"
        document.documentElement.classList.remove('dark')
    }
  }
}
</script>

<template>
  <div class="main">
    <Header :toggle="isToggle"/>
    <Hero @toggle="toggle" :isToggle="isToggle"/>
  </div>
</template>

