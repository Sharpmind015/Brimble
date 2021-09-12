<script>

export default {
  name: 'SocialItem',
  props: ['item', 'toggle']
}
</script>

<template>
  <li class="w-5">
    <a :aria-label="item.label " href="#" class="social">
      <img :src="`${item.link}-${toggle}.svg`" :alt="item.name">
    </a>
  </li>
</template>

