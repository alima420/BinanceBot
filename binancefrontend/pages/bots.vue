<template>
  <div>
    <h1>Trading Bots</h1>
    <div v-if="loading">Loading...</div>
    <div v-if="bots.length">
      <ul>
        <li v-for="bot in bots" :key="bot.id">
          {{ bot.name }} - {{ bot.trading_pair }} - {{ bot.is_active ? 'Active' : 'Inactive' }}
        </li>
      </ul>
    </div>
    <div v-else>
      <p>No bots found.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const bots = ref([])
const loading = ref(true)

const fetchBots = async () => {
  try {
    // Use the correct axios or $fetch instance here
    const response = await $fetch('http://127.0.0.1:8000/api/bots/')  // Ensure this endpoint is correct
    console.log('Fetched bots:', response) // Debug the response to check the structure
    bots.value = response  // Store the bot data in the ref
  } catch (error) {
    console.error('Error fetching bots:', error)
  } finally {
    loading.value = false  // Stop the loading state
  }
}

onMounted(() => {
  fetchBots()
})
</script>
