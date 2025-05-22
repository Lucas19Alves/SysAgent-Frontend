<script setup>
import { ref, onMounted } from 'vue'
import axios from '../axios'

const historico = ref([])
const loading = ref(false)
const erro = ref(null)

const fetchHistory = async () => {
  loading.value = true
  erro.value = null
  try {
    const res = await axios.get('/collectData/history')
    historico.value = res.data || []
  } catch (e) {
    erro.value = 'Erro ao buscar histórico de monitoramento.'
  }
  loading.value = false
}

onMounted(fetchHistory)
</script>

<template>
  <div class="h-full w-full flex flex-col bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-history text-blue-500 text-2xl"></span>
      Histórico de Monitoramento
    </h2>
    <div class="flex-1 flex flex-col">
      <div v-if="loading" class="flex-1 flex items-center justify-center text-gray-500 dark:text-gray-400">Carregando...</div>
      <div v-else-if="erro" class="flex-1 flex items-center justify-center text-red-600 dark:text-red-400">{{ erro }}</div>
      <div v-else class="flex-1 overflow-auto">
        <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
          <thead>
            <tr>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Data/Hora</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">CPU (%)</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Memória (MB)</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Disco (GB)</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in historico" :key="item.id" class="hover:bg-gray-50 dark:hover:bg-gray-900">
              <td class="px-4 py-2">{{ item.dataHora }}</td>
              <td class="px-4 py-2">{{ item.cpu }}</td>
              <td class="px-4 py-2">{{ item.memory }}</td>
              <td class="px-4 py-2">{{ item.disk }}</td>
            </tr>
            <tr v-if="historico.length === 0">
              <td colspan="4" class="text-center text-gray-500 dark:text-gray-400 py-4">Nenhum registro encontrado.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>