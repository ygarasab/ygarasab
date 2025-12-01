<template>
  <transition name="terminal">
    <div v-if="isOpen" class="about-page">
      <div class="terminal-container">
        <div class="terminal-header">
          <div class="terminal-buttons">
            <span class="terminal-btn close" @click="close"></span>
            <span class="terminal-btn minimize"></span>
            <span class="terminal-btn maximize"></span>
          </div>
          <span class="terminal-title">about.txt</span>
        </div>
        <div class="terminal-body" ref="terminalBodyRef">
          <div class="terminal-content">
            <div class="terminal-line" v-for="(line, index) in displayedText" :key="index">
              <span class="terminal-prompt" v-if="index === 0">$ </span>
              <span class="terminal-text">{{ line }}</span>
              <span class="terminal-cursor" v-if="index === displayedText.length - 1 && isTyping">_</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import { ref, watch, nextTick, onUnmounted } from 'vue'

export default {
  name: 'AboutPage',
  props: {
    isOpen: {
      type: Boolean,
      default: false
    },
    fullText: {
      type: String,
      required: true
    }
  },
  emits: ['close'],
  setup(props, { emit }) {
    const displayedText = ref([])
    const isTyping = ref(false)
    const terminalBodyRef = ref(null)
    let typingTimeout = null

    const scrollToBottom = () => {
      nextTick(() => {
        if (terminalBodyRef.value) {
          terminalBodyRef.value.scrollTop = terminalBodyRef.value.scrollHeight
        }
      })
    }

    const close = () => {
      // Cancela qualquer timeout pendente
      if (typingTimeout) {
        clearTimeout(typingTimeout)
        typingTimeout = null
      }
      // Reset completo
      displayedText.value = []
      isTyping.value = false
      emit('close')
    }

    const startTyping = () => {
      // Reset completo antes de começar
      displayedText.value = []
      isTyping.value = true
      let charIndex = 0
      
      const typeNextChar = () => {
        if (charIndex < props.fullText.length && props.isOpen) {
          const char = props.fullText[charIndex]
          
          if (displayedText.value.length === 0) {
            displayedText.value.push('')
          }
          
          const currentLineIndex = displayedText.value.length - 1
          const currentLine = displayedText.value[currentLineIndex] || ''
          
          if (currentLine.length > 85 && char === ' ') {
            displayedText.value.push('')
          } else {
            displayedText.value[currentLineIndex] = currentLine + char
          }
          
          charIndex++
          
          // Auto-scroll
          scrollToBottom()
          
          let delay = 30
          if (char === ' ') {
            delay = 20
          } else if (char === '.' || char === '!' || char === '?') {
            delay = 200
          } else if (char === ',') {
            delay = 100
          }
          
          typingTimeout = setTimeout(typeNextChar, delay)
        } else {
          isTyping.value = false
          typingTimeout = null
        }
      }
      
      typeNextChar()
    }

    watch(() => props.isOpen, (newVal) => {
      if (newVal) {
        // Pequeno delay para garantir que o DOM está pronto
        setTimeout(() => {
          startTyping()
        }, 100)
      } else {
        // Cancela timeout se estiver digitando
        if (typingTimeout) {
          clearTimeout(typingTimeout)
          typingTimeout = null
        }
        // Reset completo
        displayedText.value = []
        isTyping.value = false
      }
    })

    onUnmounted(() => {
      if (typingTimeout) {
        clearTimeout(typingTimeout)
      }
    })

    return {
      displayedText,
      isTyping,
      terminalBodyRef,
      close
    }
  }
}
</script>

<style scoped>
.about-page {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(10px);
  z-index: 10000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  overflow-y: auto;
}

.terminal-container {
  width: 100%;
  max-width: 900px;
  background: #0a0a0a;
  border: 2px solid #00ffff;
  border-radius: 8px;
  box-shadow: 0 0 30px rgba(0, 255, 255, 0.5), inset 0 0 30px rgba(0, 255, 255, 0.1);
  overflow: hidden;
}

.terminal-header {
  background: #1a1a1a;
  padding: 0.75rem 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid #00ffff;
}

.terminal-buttons {
  display: flex;
  gap: 0.5rem;
}

.terminal-btn {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  display: inline-block;
  cursor: pointer;
  transition: transform 0.2s ease, opacity 0.2s ease;
}

.terminal-btn:hover {
  transform: scale(1.1);
  opacity: 0.8;
}

.terminal-btn.close {
  background: #ff5f56;
}

.terminal-btn.minimize {
  background: #ffbd2e;
}

.terminal-btn.maximize {
  background: #27c93f;
}

.terminal-title {
  color: #00ffff;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  letter-spacing: 1px;
  flex: 1;
  text-align: center;
}


.terminal-body {
  padding: 1.5rem;
  min-height: 400px;
  max-height: 70vh;
  overflow-y: auto;
  scrollbar-width: thin;
  scrollbar-color: #00ffff #0a0a0a;
}

/* Estilização da scrollbar para WebKit (Chrome, Safari, Edge) */
.terminal-body::-webkit-scrollbar {
  width: 10px;
}

.terminal-body::-webkit-scrollbar-track {
  background: #0a0a0a;
  border-radius: 5px;
}

.terminal-body::-webkit-scrollbar-thumb {
  background: #00ffff;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
  border: 2px solid #0a0a0a;
}

.terminal-body::-webkit-scrollbar-thumb:hover {
  background: #00ff88;
  box-shadow: 0 0 15px rgba(0, 255, 136, 0.7);
}

.terminal-content {
  font-family: 'Courier New', monospace;
  font-size: 0.95rem;
  line-height: 1.8;
  color: #00ff88;
}

.terminal-line {
  margin-bottom: 0.5rem;
  display: flex;
  align-items: flex-start;
}

.terminal-prompt {
  color: #00ffff;
  margin-right: 0.5rem;
  user-select: none;
}

.terminal-text {
  color: #00ff88;
  word-wrap: break-word;
  flex: 1;
}

.terminal-cursor {
  color: #00ffff;
  animation: blink 1s infinite;
  margin-left: 2px;
}

@keyframes blink {
  0%, 50% {
    opacity: 1;
  }
  51%, 100% {
    opacity: 0;
  }
}

.terminal-enter-active,
.terminal-leave-active {
  transition: opacity 0.3s ease;
}

.terminal-enter-from,
.terminal-leave-to {
  opacity: 0;
}

@media (max-width: 768px) {
  .about-page {
    padding: 1rem;
  }

  .terminal-body {
    padding: 1rem;
    max-height: 80vh;
  }

  .terminal-content {
    font-size: 0.85rem;
    line-height: 1.6;
  }
}
</style>

