<template>
  <p>{{ msg }}</p>
</template>

<script setup>
import { defineProps } from 'vue'

defineProps({
  msg: {
    type: String,
    default: ''
  }
})
</script>

<style scoped>
p {
  font-size: 1.2rem;
}
</style>
