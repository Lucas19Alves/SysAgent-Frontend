<script setup>
import { ref } from 'vue'

const sysMonitorHost = ref(localStorage.getItem('sysmonitor_host') || '')
const sysMonitorPort = ref(localStorage.getItem('sysmonitor_port') || '')

function salvarConfig() {
  localStorage.setItem('sysmonitor_host', sysMonitorHost.value)
  localStorage.setItem('sysmonitor_port', sysMonitorPort.value)
  alert('Configuração salva!')
}
</script>

<template>
  <div id="config" class="h-full w-full flex flex-col items-center justify-center bg-white dark:bg-gray-800 rounded-xl shadow p-8">
    <h2 id="config-title" class="text-2xl font-bold mb-6 text-gray-900 dark:text-gray-100 flex items-center gap-2">
      <span class="mdi mdi-cog text-blue-500 text-2xl"></span>
      Configurações do SysMonitor
    </h2>
    <form @submit.prevent="salvarConfig" class="space-y-5 w-full max-w-md">
      <div>
        <label for="input-host" class="block mb-1 font-medium text-gray-700 dark:text-gray-200">Endereço do SysMonitor</label>
        <input
          id="input-host"
          v-model="sysMonitorHost"
          type="text"
          class="w-full border rounded-lg px-3 py-2 bg-gray-50 dark:bg-gray-900 border-gray-300 dark:border-gray-700 text-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-400 dark:focus:ring-blue-300"
          placeholder="Ex: 192.168.1.100"
          required
        />
      </div>
      <div>
        <label for="input-port" class="block mb-1 font-medium text-gray-700 dark:text-gray-200">Porta do SysMonitor</label>
        <input
          id="input-port"
          v-model="sysMonitorPort"
          type="number"
          class="w-full border rounded-lg px-3 py-2 bg-gray-50 dark:bg-gray-900 border-gray-300 dark:border-gray-700 text-gray-900 dark:text-gray-100 focus:outline-none focus:ring-2 focus:ring-blue-400 dark:focus:ring-blue-300"
          placeholder="Ex: 5001"
          required
        />
      </div>
      <button
        id="btn-salvar-config"
        type="submit"
        class="w-full bg-blue-600 hover:bg-blue-700 text-white dark:bg-blue-500 dark:hover:bg-blue-400 py-2 rounded-lg font-semibold shadow transition"
      >
        Salvar
      </button>
    </form>
  </div>
</template>