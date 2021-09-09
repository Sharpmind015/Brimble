<script>
import Heading from '../components/Heading.vue'

export default {
  name: 'Hero',
  components: {
    Heading,
  }
}
</script>

<template>
  <section class="hero">
    <Heading />
    <p class="info">Be the first to know when BRIMBLE launches</p>
    <form class="form">
      <label class="visuallyHidden" for="waitlist">
        Input your email address
      </label>
      <input placeholder="email address" class="input-mail" type="email" name="waitlist" id="waitlist">
      <input class="form-btn" type="submit" value="Join Waitlist">
    </form>
  </section>
</template>

