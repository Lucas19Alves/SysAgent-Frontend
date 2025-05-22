<script setup>
import { ref, onMounted } from 'vue'
import axios from '../axios'

const status = ref('Carregando...')
const loading = ref(false)

const fetchStatus = async () => {
  const res = await axios.get('/status')
  status.value = res.data.status || res.data || 'Desconhecido'
}

const startCollect = async () => {
  loading.value = true
  await axios.post('/collect/data/start')
  await fetchStatus()
  loading.value = false
}

const stopCollect = async () => {
  loading.value = true
  await axios.post('/collect/data/stop')
  await fetchStatus()
  loading.value = false
}

onMounted(fetchStatus)
</script>

<template>
  <div class="h-full w-full flex flex-col bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-view-dashboard text-blue-500 text-2xl"></span>
      Dashboard
    </h2>
    <div class="flex flex-col md:flex-row items-center gap-4 mb-6">
      <button
        @click="startCollect"
        :disabled="loading"
        class="px-6 py-2 bg-green-600 hover:bg-green-700 text-white rounded-lg shadow transition disabled:opacity-60"
      >
        Iniciar Coleta
      </button>
      <button
        @click="stopCollect"
        :disabled="loading"
        class="px-6 py-2 bg-red-600 hover:bg-red-700 text-white rounded-lg shadow transition disabled:opacity-60"
      >
        Parar Coleta
      </button>
      <span class="ml-4 text-lg font-medium text-gray-700 dark:text-gray-200">
        Status: <span class="font-bold">{{ status }}</span>
      </span>
    </div>
  </div>
</template>