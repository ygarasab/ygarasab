<template>
  <div class="links-container">
    <a 
      href="/curriculo_v1.pdf" 
      target="_blank"
      class="link-btn cv-link"
    >
      <span class="link-icon">[CV]</span>
      <span>Currículo</span>
    </a>
    
    <a 
      href="https://github.com/ygarasab" 
      target="_blank"
      class="link-btn github-link"
    >
      <span class="link-icon">[GH]</span>
      <span>GitHub</span>
    </a>
  </div>
</template>

<script>
export default {
  name: 'LinksSection'
}
</script>

<style scoped>
.links-container {
  display: flex;
  gap: 1.5rem;
  margin: 2rem 0;
  flex-wrap: wrap;
  justify-content: center;
}

.link-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  border: 2px solid #00ffff;
  border-radius: 8px;
  color: #00ffff;
  text-decoration: none;
  font-weight: 500;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(0, 255, 255, 0.3);
  letter-spacing: 1px;
}

.link-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.2), transparent);
  transition: left 0.5s ease;
}

.link-btn:hover::before {
  left: 100%;
}

.link-btn:hover {
  transform: translateY(-5px) scale(1.05);
  box-shadow: 0 0 20px #00ffff, 0 0 40px rgba(0, 255, 255, 0.5);
  border-color: #00ff88;
  color: #00ff88;
  background: rgba(0, 0, 0, 0.7);
}

.link-icon {
  font-size: 1.2rem;
  transition: transform 0.3s ease;
}

.link-btn:hover .link-icon {
  transform: rotate(360deg) scale(1.2);
  filter: drop-shadow(0 0 5px #00ff88);
}

@media (max-width: 768px) {
  .links-container {
    flex-direction: column;
    align-items: center;
  }
  
  .link-btn {
    width: 200px;
    justify-content: center;
  }
}
</style>

