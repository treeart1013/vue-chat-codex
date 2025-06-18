<template>
  <div class="chat-window">
    <div class="messages">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :class="['message', msg.sender]"
      >
        {{ msg.text }}
      </div>
    </div>
    <form class="input-area" @submit.prevent="handleSend">
      <input v-model="text" placeholder="Type a message..." />
      <button type="submit">Send</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
  messages: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['send'])
const text = ref('')

function handleSend() {
  if (!text.value.trim()) return
  emit('send', text.value)
  text.value = ''
}
</script>

<style scoped>
.chat-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  height: 100vh;
}
.messages {
  flex: 1;
  padding: 1rem;
  overflow-y: auto;
}
.message {
  margin-bottom: 0.5rem;
}
.message.user {
  text-align: right;
}
.input-area {
  display: flex;
  padding: 1rem;
  border-top: 1px solid #ccc;
}
.input-area input {
  flex: 1;
  padding: 0.5rem;
}
.input-area button {
  margin-left: 0.5rem;
}
</style>
