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
  width: 250px;
  background: linear-gradient(180deg, #4e54c8, #8f94fb);
  color: #fff;
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
  border-radius: 4px;
}
li.active {
  background: rgba(255, 255, 255, 0.2);
  font-weight: bold;
}
</style>
