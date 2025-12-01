<template>
  <div class="photo-container">
    <div 
      class="photo-wrapper"
      :style="{ transform: `rotate(${photoRotation}deg) scale(${photoScale})` }"
      @mouseenter="photoHover = true"
      @mouseleave="photoHover = false"
    >
      <div class="photo-ring"></div>
      <div class="photo">
        <img 
          src="/profile.jpg" 
          alt="Foto de perfil"
          @error="handleImageError"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue'

export default {
  name: 'PhotoSection',
  props: {
    photoRotation: {
      type: Number,
      default: 0
    }
  },
  setup() {
    const photoScale = ref(1)
    const photoHover = ref(false)

    const handleImageError = (e) => {
      e.target.style.display = 'none'
      e.target.parentElement.innerHTML = '<div class="placeholder-avatar">👤</div>'
    }

    let animationFrame
    onMounted(() => {
      const animate = () => {
        if (photoHover.value) {
          photoScale.value = Math.min(photoScale.value + 0.05, 1.1)
        } else {
          photoScale.value = Math.max(photoScale.value - 0.05, 1)
        }
        animationFrame = requestAnimationFrame(animate)
      }
      animate()
    })

    onUnmounted(() => {
      if (animationFrame) {
        cancelAnimationFrame(animationFrame)
      }
    })

    return {
      photoScale,
      photoHover,
      handleImageError
    }
  }
}
</script>

<style scoped>
.photo-container {
  margin: 2rem 0;
  position: relative;
}

.photo-wrapper {
  position: relative;
  transition: transform 0.3s ease;
}

.photo-ring {
  position: absolute;
  top: -10px;
  left: -10px;
  width: calc(100% + 20px);
  height: calc(100% + 20px);
  border: 3px solid #00ffff;
  border-radius: 50%;
  animation: rotate 10s linear infinite;
  box-shadow: 0 0 20px #00ffff, inset 0 0 20px #00ffff;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.photo {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid #00ffff;
  box-shadow: 0 0 30px #00ffff, 0 0 60px rgba(0, 255, 255, 0.5), inset 0 0 30px rgba(0, 255, 255, 0.2);
  background: #0a0a0a;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.photo::before {
  content: '';
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  border-radius: 50%;
  background: linear-gradient(45deg, #00ffff, #00ff88, #00ffff);
  z-index: -1;
  animation: rotate 3s linear infinite;
  opacity: 0.7;
}

.photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.placeholder-avatar {
  font-size: 80px;
  color: #00ffff;
  text-shadow: 0 0 20px #00ffff;
}

@media (max-width: 768px) {
  .photo {
    width: 150px;
    height: 150px;
  }
}
</style>

