<script setup>
import { ref, onMounted } from 'vue'
import axios from '../axios'

const schedules = ref([])
const loading = ref(false)
const erro = ref(null)

// Consulta histórico de agendamentos
const fetchSchedules = async () => {
  loading.value = true
  erro.value = null
  try {
    const res = await axios.get('/schedule/history')
    schedules.value = res.data || []
  } catch (e) {
    erro.value = 'Erro ao buscar histórico de agendamentos.'
  }
  loading.value = false
}

onMounted(fetchSchedules)
</script>

<template>
  <div id="schedule-details" class="h-full w-full flex flex-col bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 id="schedule-details-title" class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-calendar-clock text-blue-500 text-2xl"></span>
      Histórico de Agendamentos
    </h2>
    <div class="flex-1 flex flex-col">
      <div v-if="loading" class="flex-1 flex items-center justify-center text-gray-500 dark:text-gray-400">Carregando...</div>
      <div v-else-if="erro" class="flex-1 flex items-center justify-center text-red-600 dark:text-red-400">{{ erro }}</div>
      <div v-else class="flex-1 overflow-auto">
        <table id="tabela-agendamentos" class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
          <thead>
            <tr>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Servidor</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Data/Hora</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Script</th>
              <th class="px-4 py-2 text-left text-gray-700 dark:text-gray-200">Status</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in schedules" :key="item.id" class="hover:bg-gray-50 dark:hover:bg-gray-900">
              <td class="px-4 py-2">{{ item.servidor }}</td>
              <td class="px-4 py-2">{{ item.dataHora }}</td>
              <td class="px-4 py-2 truncate max-w-xs">{{ item.script }}</td>
              <td class="px-4 py-2">
                <span
                  :class="item.status === 'concluído'
                    ? 'bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 px-2 py-1 rounded'
                    : 'bg-yellow-100 dark:bg-yellow-900 text-yellow-700 dark:text-yellow-300 px-2 py-1 rounded'"
                >
                  {{ item.status || 'Pendente' }}
                </span>
              </td>
            </tr>
            <tr v-if="schedules.length === 0">
              <td colspan="4" class="text-center text-gray-500 dark:text-gray-400 py-4">Nenhum agendamento encontrado.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>