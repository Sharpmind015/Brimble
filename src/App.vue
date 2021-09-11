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
      isToggle: 'Light'
    }
  },
  methods: {
    toggle: function() {
      if(this.isToggle === 'Light') {
        gsap.to('.ellipse', {x: '-119.16px'});
        this.isToggle = "Dark";
      } else if(this.isToggle === "Dark") {
        gsap.to('.ellipse', {x: '0'});
        this.isToggle = "Light";
      }
    }
  }
}
</script>

<template>
  <div class="main">
    <Header/>
    <Hero/>
    <button v-on:click="toggle" class="toggle-switch" role="switch">
      {{isToggle}} mood
      <div class="ellipse">
        <img :src="`/src/assets/${isToggle}.png`" alt="">
      </div>  
    </button>
  </div>
</template>

