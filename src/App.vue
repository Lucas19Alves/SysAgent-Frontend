<script setup>
import { ref, onMounted } from 'vue'
import Dashboard from './components/Dashboard.vue'
import HardwareMonitor from './components/HardwareMonitor.vue'
import Config from './components/Config.vue' // Novo componente de configuração
import MonitorHistory from './components/MonitorHistory.vue'

const aba = ref('dashboard')
const abas = [
  { key: 'dashboard', label: 'Dashboard', icon: 'mdi-view-dashboard' },
  { key: 'monitor', label: 'Monitoramento', icon: 'mdi-monitor' },
  { key: 'historico', label: 'Histórico de Monitoramento', icon: 'mdi-history' },
  { key: 'config', label: 'Configurações', icon: 'mdi-cog' }
]

onMounted(() => {
  document.documentElement.classList.add('dark')
})
</script>

<template>
  <div id="app-root" class="min-h-screen transition-colors duration-300 bg-gray-900">
    <div class="max-w-5xl mx-auto">
      <!-- Header principal do sistema -->
      <header id="header" class="flex items-center justify-between py-6 mb-8">
        <h1 id="main-title" class="text-4xl font-extrabold text-center flex-1 text-transparent bg-clip-text bg-gradient-to-r from-blue-300 via-purple-300 to-pink-300 drop-shadow-lg">
          <span class="inline-flex items-center gap-2 mb-2">
            SysAgentV2 Dashboard
          </span>
        </h1>
      </header>
      <!-- Navegação de abas -->
      <nav id="main-tabs" class="flex justify-center mb-8 space-x-2">
        <button
          v-for="tab in abas"
          :key="tab.key"
          :id="`tab-${tab.key}`"
          @click="aba = tab.key"
          :class="[
            'flex items-center gap-2 px-5 py-2 rounded-lg font-semibold transition-all duration-200 border-b-2',
            aba === tab.key
              ? 'bg-gray-800 border-blue-400 text-blue-200 shadow'
              : 'bg-gray-900 border-transparent text-gray-400 hover:bg-gray-800 hover:text-blue-200'
          ]"
        >
          <span v-if="tab.icon" :class="['mdi', tab.icon, 'text-lg']"></span>
          {{ tab.label }}
        </button>
      </nav>
      <!-- Área de conteúdo principal -->
      <div id="main-content" class="rounded-xl shadow-lg p-0 min-h-[500px] h-[60vh] transition-colors duration-300 bg-gray-800 text-gray-100">
        <Dashboard v-if="aba === 'dashboard'" />
        <HardwareMonitor v-else-if="aba === 'monitor'" />
        <MonitorHistory v-else-if="aba === 'historico'" />
        <Config v-else-if="aba === 'config'" />
      </div>
      <!-- Rodapé -->
      <footer id="footer" class="mt-10 text-center text-xs text-gray-600">
        SysAgentV2 &copy; {{ new Date().getFullYear() }}
      </footer>
    </div>
  </div>
</template>

<style scoped>
@import url('https://cdn.jsdelivr.net/npm/@mdi/font@7.4.47/css/materialdesignicons.min.css');
html.dark {
  color-scheme: dark;
}
::-webkit-scrollbar {
  width: 8px;
  background: #2e3440;
}
::-webkit-scrollbar-thumb {
  background: #434c5e;
  border-radius: 4px;
}
</style>
