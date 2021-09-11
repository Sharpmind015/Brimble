<script>
import Heading from "../components/Heading.vue"
import {gsap} from 'gsap'

export default {
  name: "Hero",
  components: {
    Heading,
  },
  data() {
    return {
      tools: [
        {
          name: "vue",
          src: "/src/assets/vue.png",
        },
        {
          name: "ember",
          src: "/src/assets/ember.png",
        },
        {
          name: "react",
          src: "/src/assets/react.png",
        },
        {
          name: "nuxt",
          src: "/src/assets/nuxt.png",
        },
        {
          name: "svelte",
          src: "/src/assets/svelte.png",
        },
        {
          name: "angular",
          src: "/src/assets/angular.png",
        },
        {
          name: "next",
          src: "/src/assets/next.png",
        },
        {
          name: "javascript",
          src: "/src/assets/javascript.png",
        },
      ]
    };
  },
  mounted() {
    gsap.fromTo(`.tool-anim`, {scale: 0, rotate: 260}, {scale: 1, rotate: 0, stagger: 0.2, ease: "Bounce.out"})
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
    <Heading />
    <p class="info">Be the first to know when BRIMBLE launches</p>
    <form class="form">
      <label class="visuallyHidden" for="waitlist">
        Input your email address
      </label>
      <input
        placeholder="email address"
        class="input-mail"
        type="email"
        name="waitlist"
        id="waitlist"
      />
      <input class="form-btn" type="submit" value="Join Waitlist" />
    </form>
  </section>
</template>
