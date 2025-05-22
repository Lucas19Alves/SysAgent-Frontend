<script setup>
import { ref, onMounted } from 'vue'
import axios from '../axios'

const cpu = ref(null)
const memory = ref(null)
const disk = ref(null)

const fetchData = async () => {
  cpu.value = (await axios.get('/collectData/info/cpu')).data
  memory.value = (await axios.get('/collectData/info/memory')).data
  disk.value = (await axios.get('/collectData/info/disk')).data
}

onMounted(fetchData)
</script>

<template>
  <div class="h-full w-full flex flex-col bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-monitor text-blue-500 text-2xl"></span>
      Monitoramento de Hardware
    </h2>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 flex-1">
      <div class="p-6 border border-gray-200 dark:border-gray-700 rounded-lg bg-gray-50 dark:bg-gray-900 flex flex-col">
        <h3 class="font-semibold mb-2 text-blue-600 dark:text-blue-300">CPU</h3>
        <div v-if="cpu">
          <div class="text-lg">Uso: <span class="font-bold">{{ cpu.usage }}%</span></div>
          <div>Núcleos: {{ cpu.cores }}</div>
        </div>
        <div v-else class="text-gray-400">Carregando...</div>
      </div>
      <div class="p-6 border border-gray-200 dark:border-gray-700 rounded-lg bg-gray-50 dark:bg-gray-900 flex flex-col">
        <h3 class="font-semibold mb-2 text-purple-600 dark:text-purple-300">Memória</h3>
        <div v-if="memory">
          <div>Total: {{ memory.total }} MB</div>
          <div>Usada: {{ memory.used }} MB</div>
          <div>Disponível: {{ memory.free }} MB</div>
        </div>
        <div v-else class="text-gray-400">Carregando...</div>
      </div>
      <div class="p-6 border border-gray-200 dark:border-gray-700 rounded-lg bg-gray-50 dark:bg-gray-900 flex flex-col">
        <h3 class="font-semibold mb-2 text-pink-600 dark:text-pink-300">Disco</h3>
        <div v-if="disk">
          <div>Total: {{ disk.total }} GB</div>
          <div>Usado: {{ disk.used }} GB</div>
          <div>Disponível: {{ disk.free }} GB</div>
        </div>
        <div v-else class="text-gray-400">Carregando...</div>
      </div>
    </div>
  </div>
</template>