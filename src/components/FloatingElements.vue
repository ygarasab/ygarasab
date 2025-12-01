<template>
  <div 
    v-for="i in 5" 
    :key="i"
    class="floating-element"
    :style="getFloatingStyle(i)"
  ></div>
</template>

<script>
export default {
  name: 'FloatingElements',
  methods: {
    getFloatingStyle(index) {
      const delay = index * 0.5
      const duration = 3 + (index * 0.5)
      return {
        animationDelay: `${delay}s`,
        animationDuration: `${duration}s`,
        left: `${20 + index * 15}%`,
        top: `${10 + index * 10}%`,
      }
    }
  }
}
</script>

<style scoped>
.floating-element {
  position: absolute;
  width: 8px;
  height: 8px;
  background: #00ffff;
  border-radius: 50%;
  pointer-events: none;
  animation: floatAround 6s ease-in-out infinite;
  box-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
}

@keyframes floatAround {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0.5;
    box-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
  }
  25% {
    transform: translate(30px, -30px) scale(1.5);
    opacity: 1;
    box-shadow: 0 0 15px #00ffff, 0 0 30px #00ffff, 0 0 45px #00ffff;
  }
  50% {
    transform: translate(-20px, -50px) scale(0.8);
    opacity: 0.3;
    box-shadow: 0 0 5px #00ffff;
  }
  75% {
    transform: translate(40px, -20px) scale(1.2);
    opacity: 0.7;
    box-shadow: 0 0 12px #00ffff, 0 0 25px #00ffff;
  }
}
</style>

