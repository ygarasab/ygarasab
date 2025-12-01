<template>
  <div class="construction-message">
    <p class="construction-text">
      &gt; CONSTRUINDO...
    </p>
    <p class="construction-subtext">
      Portfólio em desenvolvimento. Retorne em breve para atualizações.
    </p>
  </div>
</template>

<script>
export default {
  name: 'ConstructionMessage'
}
</script>

<style scoped>
.construction-message {
  text-align: center;
  margin-bottom: 3rem;
  animation: fadeInDown 1s ease;
}

.construction-text {
  font-size: 1.5rem;
  color: #00ffff;
  font-weight: 600;
  margin-bottom: 0.5rem;
  text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff, 0 0 30px #00ffff;
  animation: pulse 2s ease-in-out infinite;
  letter-spacing: 2px;
}

.construction-subtext {
  font-size: 1rem;
  color: #00ff88;
  text-shadow: 0 0 5px #00ff88;
  letter-spacing: 1px;
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
    text-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff, 0 0 30px #00ffff;
  }
  50% {
    transform: scale(1.05);
    text-shadow: 0 0 15px #00ffff, 0 0 30px #00ffff, 0 0 45px #00ffff;
  }
}

@keyframes fadeInDown {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .construction-text {
    font-size: 1.2rem;
  }
}
</style>

