# SysAgentV2 Dashboard

Painel moderno para monitoramento e agendamento de tarefas do agente SysAgentV2.

# SysAgentV2 - [Kaio](https://github.com/Kaio1394).

Acesse o repositório do [SysAgentV2](https://github.com/Kaio1394/SysAgentV2).

## ✨ Sobre

Este projeto é um frontend em **Vue 3 + Vite** com Tailwind CSS para monitorar hardware, agendar tarefas e visualizar históricos de execução do agente SysAgentV2.

## 🚀 Funcionalidades

- **Dashboard**: Status do agente e controle de coleta de dados.
- **Monitoramento**: Visualização em tempo real de CPU, memória e disco.
- **Agendar Tarefa**: Formulário para agendamento de scripts/tarefas.
- **Histórico de Agendamentos**: Lista de tarefas agendadas e seus status.
- **Histórico de Monitoramento**: Registros de uso de hardware ao longo do tempo.

## 🖥️ Tecnologias

- [Vue 3](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [Tailwind CSS](https://tailwindcss.com/)
- [Axios](https://axios-http.com/)
- [Material Design Icons](https://pictogrammers.com/library/mdi/)

## ⚡ Instalação

```bash
git clone https://github.com/Lucas19Alves/SysAgent-Frontend
cd SysAgent-Frontend
npm install
npm run dev
```

Acesse em [http://localhost:5173](http://localhost:5173)

## ⚙️ Configuração da API

Por padrão, o frontend espera a API rodando em `http://localhost:5000`.  
Altere o arquivo `src/axios.js`.

## 📂 Estrutura de Pastas

```
src/
  components/
    Dashboard.vue
    HardwareMonitor.vue
    Schedule.vue
    ScheduleDetails.vue
    MonitorHistory.vue
  App.vue
  main.js
  axios.js
```

## 📝 Endpoints esperados da API

- `GET /status` — Status do agente
- `POST /collect/data/start` — Inicia coleta
- `POST /collect/data/stop` — Para coleta
- `GET /collectData/info/cpu` — Dados CPU
- `GET /collectData/info/memory` — Dados Memória
- `GET /collectData/info/disk` — Dados Disco
- `GET /schedule/history` — Histórico de agendamentos
- `POST /schedule/task` — Agendar tarefa
- `GET /collectData/history` — Histórico de monitoramento


## 📄 Licença

MIT

---

> Desenvolvido por Lucas
