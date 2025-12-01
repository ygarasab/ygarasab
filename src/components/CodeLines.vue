<template>
  <div class="code-lines">
    <div class="code-line" v-for="i in 3" :key="'line-' + i" :style="getCodeLineStyle(i)">
      <span class="code-symbol">></span>
      <span class="code-text">{{ getCodeText(i) }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CodeLines',
  methods: {
    getCodeLineStyle(index) {
      return {
        left: `${10 + index * 30}%`,
        top: `${15 + index * 25}%`,
        animationDelay: `${index * 0.8}s`,
      }
    },
    getCodeText(index) {
      const texts = [
        'const portfolio = new Portfolio();',
        'portfolio.status = "building";',
        'return "coming_soon";'
      ]
      return texts[index - 1] || ''
    }
  }
}
</script>

<style scoped>
.code-lines {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  pointer-events: none;
  z-index: 0;
  opacity: 0.3;
}

.code-line {
  position: absolute;
  font-family: 'Courier New', monospace;
  font-size: 0.8rem;
  color: #00ff88;
  white-space: nowrap;
  animation: codeFade 4s ease-in-out infinite;
  text-shadow: 0 0 5px #00ff88;
}

.code-symbol {
  color: #00ffff;
  margin-right: 0.5rem;
  text-shadow: 0 0 5px #00ffff;
}

.code-text {
  color: #00ff88;
}

@keyframes codeFade {
  0%, 100% {
    opacity: 0.2;
    transform: translateX(-10px);
  }
  50% {
    opacity: 0.5;
    transform: translateX(0);
  }
}
</style>

