<script
>
import Header from "./layouts/Header.vue";

export default {
  name: 'App',
  components: {
    Header
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
  </div>
</template>

