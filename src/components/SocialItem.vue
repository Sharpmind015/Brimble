<script>

export default {
  name: 'SocialItem',
  props: ['item']
}
</script>

<template>
  <li class=" w-5">
    <a :aria-label="item.label" href="#" class="">
      <img :src="item.link" :alt="item.name">
    </a>
  </li>
</template>

