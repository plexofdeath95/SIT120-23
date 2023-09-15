<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps<{ someProp: string }>()
const receivedProp = ref(props.someProp)

const emit = defineEmits()

const sendEvent = () => {
  emit('child-event', 'Hello from Child!')
}
</script>

<template>
  <div>
    <p>{{ receivedProp }}</p>
    <button @click="sendEvent">Send Event</button>
    <slot></slot>
  </div>
</template>
