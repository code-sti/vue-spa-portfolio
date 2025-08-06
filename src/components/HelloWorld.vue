<script setup lang="ts">
import { ref, onMounted } from 'vue'

defineProps<{
  msg: string
}>()

// State
const apiMessage = ref('Loading...')

// Fetch from Laravel
onMounted(async () => {
  try {
    const res = await fetch('/api/hello')
    const data = await res.json()
    apiMessage.value = data.message
  } catch (e) {
    apiMessage.value = 'Failed to fetch message'
    console.error(e)
  }
})
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a project with
      <a href="https://vite.dev/" target="_blank" rel="noopener">Vite</a> +
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue 3</a>. What's next?
    </h3>


    <div class="mt-4 text-center">
      <p class="text-blue-600 font-medium">API says: {{ apiMessage }}</p>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
