<template>
  <footer class="footer">
    <p>@ygarasab</p>
  </footer>
</template>

<script>
export default {
  name: 'FooterComponent'
}
</script>

<style scoped>
.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 1.5rem;
  text-align: center;
  z-index: 100;
  pointer-events: none;
}

.footer p {
  color: #00ffff;
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  letter-spacing: 2px;
  text-shadow: 0 0 10px #00ffff, 0 0 20px rgba(0, 255, 255, 0.5);
  opacity: 0.8;
  transition: opacity 0.3s ease;
}

.footer p:hover {
  opacity: 1;
  text-shadow: 0 0 15px #00ffff, 0 0 30px #00ffff;
}

@media (max-width: 768px) {
  .footer {
    padding: 1rem;
  }

  .footer p {
    font-size: 0.8rem;
  }
}
</style>

