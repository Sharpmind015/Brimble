<script
>
import Header from "./layouts/Header.vue";
import Hero from "./layouts/Hero.vue";

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
      ]
    }
  }
}
</script>

<template>
  <div class="main">
    <Header/>
    <Hero/>
  </div>
</template>

