<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
});
</script>

<template>
  <h1 class="text-blue-600 text-4xl bg-yellow-300 text-center font-bold">{{ msg }}</h1>
</template>

