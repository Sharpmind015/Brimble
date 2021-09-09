<script>

export default {
  name: 'NavItem',
  props: ['item']
}
</script>

<template>
  <li class="uppercase mr-7 lg:mr-18 xl:mr-24">
    <a :href="item.link" :class="item.isActive ? 'btn' : 'link'">
      {{item.name}}
    </a>
  </li>
</template>

