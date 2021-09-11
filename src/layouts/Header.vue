<script>
import { gsap } from "gsap";
import NavItem from "../components/NavItem.vue";
import SocialItem from "../components/SocialItem.vue";

export default {
  name: 'Home',
  components: {
    NavItem,
    SocialItem
  },
  data() {
    return {
      items: [
        {
          name: 'Home',
          link: '#',
          isActive: true
        },
        {
          name: 'Pricing',
          link: '#',
          isActive: false
        },
        {
          name: 'About',
          link: '#',
          isActive: false
        },
        {
          name: 'Framework',
          link: '#',
          isActive: false
        }
      ],
      socialLinks: [
        {
          name: 'Github',
          link: '/src/assets/github.png',
          label: 'View brimble github repo'
        },
        {
          name: 'Twitter',
          link: '/src/assets/twitter.png',
          label: 'View brimble twitter profile'
        }
      ]
    }
  },
  mounted() {
    window.tl = gsap.timeline({paused: true});
    tl.to('.line-2', {x: '-11px',y: '-15px',rotate: 45, duration: 1, ease: "expo.out"})
    .to('.line-1', {x: '-12px',y: '7px',rotate: -45, duration: 1, ease: "expo.out"}, "-=1")
    .to('.nav-bg', {top: 0, duration: 1, ease: "Power3.out"}, "-=1")
    .to('.nav-mobile', {top: 0, duration: 0.9, ease: "Power3.out"}, '-=0.9')
    tl.reverse()
  },
  methods: {
    menuAnim: function() {
      tl.reversed() ? tl.play() : tl.reverse();
    }
  }
}
</script>

<template>
  <header class="header">
    <img class=" w-24 " src="../assets/Brimble.png" alt="Bimble logo">
    <button v-on:click="menuAnim" aria-label="Click to open main menu" class="menu-btn">
      <span class="line line-1"></span>
      <span class="line line-2"></span>
    </button>  
    <nav class=" w-3/4 btw-center hidden md:flex ">
    <ul class="flex btw-center " role="list">
      <NavItem :key="index" :item="item" v-for="(item, index) in items" />
    </ul>
    <ul class="flex btw-center md:space-x-8 lg:space-x-20" role="list">
      <SocialItem :key="index" :item="link" v-for="(link, index) in socialLinks"></SocialItem>
    </ul>
    </nav>
    <nav class="nav-mobile">
    <ul class="menu-mobile" role="list">
      <NavItem :key="index" :item="item" v-for="(item, index) in items" />
    </ul>
    </nav>
    <div class="nav-bg"></div>
  </header>
</template>

