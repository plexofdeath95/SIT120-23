<!-- App.vue -->
<script setup lang="ts">
import { ref, computed, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import ChildComponent from './components/ChildComponent.vue'

const message = ref<string>('Hello, Vue!')
const counter = ref<number>(0)
const isActive = ref<boolean>(true)
const activeColor = ref<string>('red')
const myObject = ref<Record<string, number>>({ a: 1, b: 2, c: 3 })
const rawHtml = ref<string>('<span style="color: red">This is raw HTML</span>')
const dynamicId = ref<string>('myId')

const doubleCounter = computed(() => counter.value * 2)
//9. Watchers
watch(counter, (newVal: number, oldVal: number) => {
  console.log(`New: ${newVal}, Old: ${oldVal}`)
})

const increment = (): void => {
  counter.value++
}

const decrement = (): void => {
  counter.value--
}

const handleChildEvent = (eventMessage: string): void => {
  console.log('Received child event:', eventMessage)
}

const route = useRoute()
const router = useRouter()
</script>

<template>
  <!-- 1. Template Syntax -->
  <div>
    <!-- 1.a Text Interpolation -->
    <p>{{ message }}</p>

    <!-- 1.b Raw HTML -->
    <div v-html="rawHtml"></div>

    <!-- 1.c Attribute Bindings -->
    <div v-bind:id="dynamicId">Attribute Binding</div>

    <!-- 1.d JavaScript expressions -->
    <p>{{ counter * 2 }}</p>

    <!-- 2. Methods -->
    <button @click="increment">Increment</button>

    <!-- 5. Class and Style Bindings -->
    <div v-bind:class="{ active: isActive }">Class Binding</div>
    <div v-bind:style="{ color: activeColor }">Style Binding</div>

    <!-- 6. List Rendering -->
    <ul>
      <!-- 6.a v-for with an Object -->
      <li v-for="(value, key) in myObject" :key="key">{{ key }}: {{ value }}</li>
    </ul>

    <!-- 6.b v-for with a Range -->
    <div v-for="n in 3">{{ n }}</div>

    <!-- 7. Event Handling -->
    <!-- 7.a Inline Handlers -->
    <button @click="counter += 1">Add 1</button>

    <!-- 7.b Method Handlers -->
    <button @click="decrement">Decrement</button>

    <!-- 8. Form Input Bindings -->
    <input v-model="message" type="text" />

    <!-- 10. Components -->
    <ChildComponent :some-prop="message" @child-event="handleChildEvent">
      <!-- 10.c Slots -->
      <span>This is a slot content</span>
    </ChildComponent>

    <!-- 11. Router -->
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
    <router-view></router-view>
  </div>
</template>

<style>
/* 5.a Class and Style Bindings */
.active {
  background-color: green;
}
</style>
