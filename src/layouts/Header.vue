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
          link: '/src/assets/github',
          label: 'View brimble github repo'
        },
        {
          name: 'Twitter',
          link: '/src/assets/twitter',
          label: 'View brimble twitter profile'
        }
      ]
    }
  },
  props: ['toggle'],
  mounted() {
    window.tl = gsap.timeline({paused: true});
    tl.to('.line-2', {x: '-11px',y: '-15px',rotate: 45, duration: 1, ease: "expo.out"})
    .to('.line-1', {x: '-12px',y: '7px',rotate: -45, duration: 1, ease: "expo.out"}, "-=1")
    .to('.nav-bg', {top: 0, duration: 1, ease: "Power3.out"}, "-=1")
    .to('.nav-mobile', {top: 0, duration: 0.9, ease: "Power3.out"}, '-=0.9')
    .fromTo('.link-anim',{y: '50px'}, {y: 0,stagger: 0.2, ease: "expo.out"}, "-0.1")
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
    <a href="index.html">
      <img class=" w-24 " :src="`/src/assets/brimble-${toggle}.svg`" alt="Bimble logo">
    </a>
    <button v-on:click="menuAnim" aria-label="Click to open main menu" class="menu-btn">
      <span class="line line-1"></span>
      <span class="line line-2"></span>
    </button>  
    <nav class=" w-3/4 btw-center hidden md:flex ">
    <ul class="flex btw-center " role="list">
      <NavItem :mobile="false" :key="index" :item="item" v-for="(item, index) in items" />
    </ul>
    <ul class="flex btw-center md:space-x-8 lg:space-x-20" role="list">
      <SocialItem :toggle="toggle" :key="index" :item="link" v-for="(link, index) in socialLinks"></SocialItem>
    </ul>
    </nav>
    <nav class="nav-mobile">
    <ul class="menu-mobile" role="list">
      <NavItem :mobile="true" :key="index" :item="item" v-for="(item, index) in items" />
    </ul>
    </nav>
    <div class="nav-bg"></div>
  </header>
</template>

