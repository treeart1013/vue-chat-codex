<template>
  <div class="sidebar">
    <h2>Conversations</h2>
    <ul>
      <li
        v-for="conv in conversations"
        :key="conv.id"
        :class="{ active: conv.id === selectedId }"
        @click="$emit('select', conv.id)"
      >
        {{ conv.title }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  conversations: {
    type: Array,
    required: true
  },
  selectedId: {
    type: Number,
    required: true
  }
})

defineEmits(['select'])
</script>

<style scoped>
.sidebar {
  width: 200px;
  border-right: 1px solid #ccc;
  padding: 1rem;
}
ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  padding: 0.5rem;
  cursor: pointer;
}
li.active {
  background: #eee;
  font-weight: bold;
}
</style>
