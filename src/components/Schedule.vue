<script setup>
import { ref } from 'vue'
import axios from '../axios'

const form = ref({
  servidor: '',
  dataHora: '',
  script: ''
})

const loading = ref(false)
const mensagem = ref(null)
const tipoMensagem = ref('')

// Envia agendamento para o backend
const agendar = async () => {
  mensagem.value = null
  tipoMensagem.value = ''
  loading.value = true
  try {
    await axios.post('/schedule/task', {
      servidor: form.value.servidor,
      dataHora: form.value.dataHora,
      script: form.value.script
    })
    mensagem.value = 'Tarefa agendada com sucesso!'
    tipoMensagem.value = 'sucesso'
    form.value.servidor = ''
    form.value.dataHora = ''
    form.value.script = ''
  } catch (e) {
    mensagem.value = 'Erro ao agendar tarefa.'
    tipoMensagem.value = 'erro'
  }
  loading.value = false
}
</script>

<template>
  <div id="schedule" class="h-full w-full flex flex-col items-center justify-center bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 id="schedule-title" class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-calendar-plus text-blue-500 text-2xl"></span>
      Agendamento de Tarefa
    </h2>
    <form id="form-agendamento" @submit.prevent="agendar" class="space-y-5 w-full max-w-lg">
      <div>
        <label for="input-servidor" class="block mb-1 font-medium text-gray-700 dark:text-gray-200">Nome do servidor</label>
        <input
          id="input-servidor"
          v-model="form.servidor"
          type="text"
          class="w-full border rounded-lg px-3 py-2 bg-gray-50 dark:bg-gray-900 border-gray-300 dark:border-gray-700 text-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-400 dark:focus:ring-blue-300"
          required
        />
      </div>
      <div>
        <label for="input-datahora" class="block mb-1 font-medium text-gray-700 dark:text-gray-200">Data e hora</label>
        <input
          id="input-datahora"
          v-model="form.dataHora"
          type="datetime-local"
          class="w-full border rounded-lg px-3 py-2 bg-gray-50 dark:bg-gray-900 border-gray-300 dark:border-gray-700 text-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-400 dark:focus:ring-blue-300"
          required
        />
      </div>
      <div>
        <label for="input-script" class="block mb-1 font-medium text-gray-700 dark:text-gray-200">Script a ser executado</label>
        <textarea
          id="input-script"
          v-model="form.script"
          rows="4"
          class="w-full border rounded-lg px-3 py-2 bg-gray-50 dark:bg-gray-900 border-gray-300 dark:border-gray-700 text-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-400 dark:focus:ring-blue-300"
          required
        ></textarea>
      </div>
      <button
        id="btn-agendar"
        type="submit"
        class="w-full bg-blue-600 hover:bg-blue-700 text-white dark:bg-blue-500 dark:hover:bg-blue-400 py-2 rounded-lg font-semibold shadow transition disabled:opacity-60"
        :disabled="loading"
      >
        {{ loading ? 'Agendando...' : 'Agendar' }}
      </button>
    </form>
    <div v-if="mensagem" class="mt-4 text-center">
      <span
        id="msg-agendamento"
        :class="tipoMensagem === 'sucesso'
          ? 'bg-green-100 dark:bg-green-900 text-green-700 dark:text-green-300 px-4 py-2 rounded'
          : 'bg-red-100 dark:bg-red-900 text-red-700 dark:text-red-300 px-4 py-2 rounded'"
      >
        {{ mensagem }}
      </span>
    </div>
  </div>
</template>