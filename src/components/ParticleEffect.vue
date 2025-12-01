<template>
  <div 
    v-for="(particle, index) in particles" 
    :key="'particle-' + index"
    class="particle"
    :style="{
      left: particle.x + 'px',
      top: particle.y + 'px',
      '--endX': particle.endX + 'px',
      '--endY': particle.endY + 'px',
      '--delay': particle.delay + 's',
      '--color': particle.color
    }"
  ></div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'ParticleEffect',
  setup(props, { expose }) {
    const particles = ref([])

    const createParticles = (e) => {
      const colors = ['#00ffff', '#00ff88', '#00ffff', '#00ff88', '#00ffff']
      const particleCount = 20
      
      for (let i = 0; i < particleCount; i++) {
        const angle = (360 / particleCount) * i
        const distance = 60 + Math.random() * 120
        const delay = Math.random() * 0.2
        const angleRad = (angle * Math.PI) / 180
        
        const endX = Math.cos(angleRad) * distance
        const endY = Math.sin(angleRad) * distance
        
        particles.value.push({
          x: e.clientX,
          y: e.clientY,
          endX: endX,
          endY: endY,
          delay: delay,
          color: colors[i % colors.length],
          id: Date.now() + i
        })
      }

      setTimeout(() => {
        particles.value = particles.value.filter(p => {
          const particleAge = Date.now() - p.id
          return particleAge < 1500
        })
      }, 1500)
    }

    expose({
      createParticles
    })

    return {
      particles
    }
  }
}
</script>

<style scoped>
.particle {
  position: fixed;
  width: 8px;
  height: 8px;
  background: var(--color);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
  box-shadow: 0 0 15px var(--color), 0 0 30px var(--color), 0 0 45px var(--color);
  animation: particleExplode 1.2s ease-out forwards;
  animation-delay: var(--delay);
  opacity: 1;
}

@keyframes particleExplode {
  0% {
    transform: translate(-50%, -50%) translate(0, 0) scale(1);
    opacity: 1;
    box-shadow: 0 0 15px var(--color), 0 0 30px var(--color), 0 0 45px var(--color);
  }
  50% {
    opacity: 0.9;
    box-shadow: 0 0 10px var(--color), 0 0 20px var(--color);
  }
  100% {
    transform: translate(-50%, -50%) translate(var(--endX), var(--endY)) scale(0);
    opacity: 0;
    box-shadow: 0 0 5px var(--color);
  }
}
</style>

