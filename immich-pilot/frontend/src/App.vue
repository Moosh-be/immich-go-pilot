<template>
  <div class="terminal-app">
    <div class="terminal">
      <div class="terminal-titlebar">
        <div class="terminal-dots">
          <span class="dot red"></span>
          <span class="dot yellow"></span>
          <span class="dot green"></span>
        </div>
        <span class="terminal-title">immich-pilot</span>
      </div>
      <div class="terminal-body" ref="terminalBody">
        <div class="line" v-for="(line, i) in lines" :key="i" :class="line.type">
          <span v-if="line.type === 'prompt'">{{ line.content }}</span>
          <span v-else>{{ line.content }}</span>
        </div>
        <div class="line input-line">
          <span class="prompt-text">$ </span>
          <input
            ref="commandInput"
            v-model="command"
            @keyup.enter="execute"
            class="command-input"
            autocomplete="off"
            spellcheck="false"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
import { Help } from '@wails/go/main/App.js'

const command = ref('')
const lines = ref([
  { content: 'immich-pilot - Interface pour immich-go', type: 'info' },
  { content: 'Tapez une commande et appuyez sur Entrée.', type: 'info' },
  { content: '', type: '' },
])
const terminalBody = ref(null)
const commandInput = ref(null)

async function execute() {
  const cmd = command.value.trim()
  if (!cmd) return

  // Afficher la commande saisie
  lines.value.push({ content: cmd, type: 'input' })
  command.value = ''

  // Afficher le chargement
  lines.value.push({ content: '...', type: 'loading' })
  await scrollToBottom()

  if (cmd === 'help' || cmd === '-h' || cmd === '--help') {
    try {
      const result = await Help()
      result.split('\n').forEach(line => {
        lines.value.push({ content: line, type: 'output' })
      })
    } catch (err) {
      lines.value.push({ content: `Erreur: ${err}`, type: 'error' })
    }
  } else {
    lines.value.push({ content: `Commande: ${cmd}`, type: 'output' })
  }

  await scrollToBottom()
}

function scrollToBottom() {
  return nextTick(() => {
    if (terminalBody.value) {
      terminalBody.value.scrollTop = terminalBody.value.scrollHeight
    }
  })
}
</script>

<style scoped>
.terminal-app {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #1a1b26;
}

.terminal {
  width: 90%;
  max-width: 900px;
  height: 70vh;
  background-color: #24283b;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.4);
  display: flex;
  flex-direction: column;
}

.terminal-titlebar {
  background-color: #1a1b26;
  padding: 8px 16px;
  display: flex;
  align-items: center;
  gap: 12px;
  border-bottom: 1px solid #363a50;
}

.terminal-dots {
  display: flex;
  gap: 6px;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}

.dot.red { background-color: #ff5f57; }
.dot.yellow { background-color: #febc2e; }
.dot.green { background-color: #28c840; }

.terminal-title {
  color: #7aa2f7;
  font-size: 13px;
  font-family: monospace;
}

.terminal-body {
  flex: 1;
  padding: 12px 16px;
  overflow-y: auto;
  font-family: 'Cascadia Code', 'Fira Code', 'Consolas', monospace;
  font-size: 14px;
  line-height: 1.6;
  color: #9aa5ce;
  cursor: text;
}

.line {
  white-space: pre-wrap;
  word-break: break-all;
}

.line.output {
  color: #7dcfff;
}

.line.error {
  color: #f7768e;
}

.line.loading {
  color: #7aa2f7;
  font-style: italic;
}

.line.info {
  color: #9e6fda;
}

.line.prompt {
  color: #7aa2f7;
}

.input-line {
  display: flex;
  align-items: center;
  margin-top: 4px;
}

.prompt-text {
  color: #7aa2f7;
}

.command-input {
  flex: 1;
  background: transparent;
  border: none;
  outline: none;
  color: #c0caf5;
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}

.command-input::selection {
  background-color: #3d4570;
}
</style>
