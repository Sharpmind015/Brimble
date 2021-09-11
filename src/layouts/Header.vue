<script>
import { ref } from "vue";
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
  }
  // props: 'menu'
}
</script>

<template>
  <header class="header">
    <img class=" w-24 " src="../assets/Brimble.png" alt="Bimble logo">
    <button aria-label="Click to open main menu" class="menu-btn"></button>  
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
  </header>
</template>

