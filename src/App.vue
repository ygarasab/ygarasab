<template>
  <div class="container" @mousemove="handleMouseMove" @click="handleClick">
    <!-- Cursor personalizado -->
    <div 
      class="cursor" 
      :style="{ left: cursorX + 'px', top: cursorY + 'px' }"
    ></div>

    <!-- Mensagem de construção -->
    <ConstructionMessage />

    <!-- Foto circular -->
    <PhotoSection :photo-rotation="photoRotation" />

    <!-- Links -->
    <LinksSection />

    <!-- Botão About -->
    <button 
      class="personal-btn"
      @click="openAboutPage"
      @mouseenter="buttonHover = true"
      @mouseleave="buttonHover = false"
    >
      [ABOUT]
    </button>

    <!-- Página About -->
    <AboutPage 
      :is-open="showAboutPage" 
      :full-text="fullText"
      @close="closeAboutPage"
    />

    <!-- Elementos decorativos -->
    <FloatingElements />
    <CodeLines />

    <!-- Partículas de click -->
    <ParticleEffect ref="particleEffectRef" />

    <!-- Rodapé -->
    <FooterComponent />
  </div>
</template>

<script>
import { ref } from 'vue'
import ConstructionMessage from './components/ConstructionMessage.vue'
import PhotoSection from './components/PhotoSection.vue'
import LinksSection from './components/LinksSection.vue'
import AboutPage from './components/AboutPage.vue'
import FloatingElements from './components/FloatingElements.vue'
import CodeLines from './components/CodeLines.vue'
import ParticleEffect from './components/ParticleEffect.vue'
import FooterComponent from './components/FooterComponent.vue'

export default {
  name: 'App',
  components: {
    ConstructionMessage,
    PhotoSection,
    LinksSection,
    AboutPage,
    FloatingElements,
    CodeLines,
    ParticleEffect,
    FooterComponent
  },
  setup() {
    const cursorX = ref(0)
    const cursorY = ref(0)
    const photoRotation = ref(0)
    const buttonHover = ref(false)
    const showAboutPage = ref(false)
    const particleEffectRef = ref(null)
    
    const fullText = `Oi! Desculpa a bagunça, que é a primeira vez que eu preciso fazer um... 
        Não, não é a primeira vez que eu preciso fazer, é a primeira vez que eu me empenho em fazer um portfólio. 
        É um desafio, eu acho, porque as minhas atividades são muito mais de back, muito mais com ciência de dados. 
        Eu não tenho certeza de como traduzir isso para um portfólio. Visualmente, eu acho que os meus amigos front-end conseguem demonstrar muito mais aqui. 
        Não que eu não saiba front-end, mas é que não é tanto o meu foco, por mais que aqui possa parecer. 
        E tem outra coisa, depois que a gente é contratado, para que serve o portfólio? Eu deixo ele em pé? Eu não sei, eu tenho esse domínio aqui. 
        Eu estou pensando em, talvez, depois mudar ele para ser algum tipo de coisa útil para mim no dia-a-dia, tipo... Ah, remove o fundo, codifica isso aqui, 
        decodifica isso aqui, renderiza esse HTML, sabe, esse tipo de coisa que dá para usar no dia-a-dia? 
        Eu não tenho que ficar dependendo dos sites terceiros, não sei. 
        Mas eu não sei o que fazer sobre esse portfólio aqui não, cara. 
        Eu acho que eu vou adicionar alguns gráficos, talvez alguma coisa mais interativa para demonstrar minha proeza de dados. Não tenho certeza. 
        Essa foto também, eu não gosto muito dessa foto. Eu botei ela porque ela é mais recente, ela é de frente. Eu não tenho tantas fotos minhas mais recentes. 
        Eu tenho algumas fotos que eu uso no LinkedIn, que são de uma viagem de 2023, mas eu não sei se é uma boa deixar aqui. Talvez eu deixe, não sei. 
        Meu currículo também tá complicado. Não sei se alguém clicou para abrir meu currículo. 
        Talvez eu tenha atualizado já, mas a V1 do meu currículo ainda não está... ideal. 
        Talvez eu precise fazer algo melhor, talvez adicionar algum estilo, não está tão bem construído. 
        Mas isso vem uma ansiedade de entrar logo no pipe e começar a ver que tipo de vagas a gente tem por aí. E partir para essa nova jornada. 
        Não sei ainda que tipo de trabalho eu estou procurando. Mas eu queria uma empresa bem estruturada, eu queria ter algum lugar com uma boa liderança. 
        Todas as empresas que eu trabalhei até agora eu meio que tive que ser exército de um homem só, ou a pessoa que sabe o que tem que ser feito e tal. 
        E isso dificulta muito a evolução, eu acho que isso... Não ter essa visão do topo, de uma boa referência, sabe? 
        Eu acho que isso, não sei se me desmotiva, mas me tira o foco, ou não me dá foco, sei lá. 
        Então seria legal uma empresa talvez mais estabilizada eu ter essa visão desse cara, essa referência. Enfim. Bora lá.`

    const handleMouseMove = (e) => {
      cursorX.value = e.clientX
      cursorY.value = e.clientY
      
      // Efeito parallax na foto
      const centerX = window.innerWidth / 2
      const centerY = window.innerHeight / 2
      const deltaX = (e.clientX - centerX) / 50
      
      photoRotation.value = deltaX * 0.5
    }

    const handleClick = (e) => {
      if (particleEffectRef.value) {
        particleEffectRef.value.createParticles(e)
      }
    }

    const openAboutPage = () => {
      showAboutPage.value = true
    }

    const closeAboutPage = () => {
      showAboutPage.value = false
    }

    return {
      cursorX,
      cursorY,
      photoRotation,
      buttonHover,
      showAboutPage,
      fullText,
      particleEffectRef,
      handleMouseMove,
      handleClick,
      openAboutPage,
      closeAboutPage
    }
  }
}
</script>

<style scoped>
.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  position: relative;
  z-index: 1;
}

.cursor {
  position: fixed;
  width: 20px;
  height: 20px;
  border: 2px solid #00ffff;
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  transition: transform 0.1s ease;
  z-index: 9999;
  box-shadow: 0 0 10px #00ffff, 0 0 20px #00ffff;
}

.personal-btn {
  margin-top: 1.5rem;
  padding: 0.75rem 2rem;
  background: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(10px);
  border: 2px solid #00ff88;
  border-radius: 8px;
  color: #00ff88;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 0 15px rgba(0, 255, 136, 0.4);
  letter-spacing: 1px;
  font-family: 'Courier New', monospace;
}

.personal-btn:hover {
  transform: translateY(-3px) scale(1.05);
  background: rgba(0, 0, 0, 0.7);
  box-shadow: 0 0 25px #00ff88, 0 0 50px rgba(0, 255, 136, 0.5);
  border-color: #00ffff;
  color: #00ffff;
}
</style>
