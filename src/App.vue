<template>
  <div class="page">
    <header class="topbar">
      <div class="brand">YGARASAB</div>
      <div class="topbar-right">
        <nav class="menu">
          <a href="#about">{{ t.navAbout }}</a>
          <a href="#focus">{{ t.navFocus }}</a>
          <a href="#projects">{{ t.navProjects }}</a>
          <a href="#contact">{{ t.navContact }}</a>
        </nav>
        <button class="lang-switch" @click="toggleLocale">
          {{ locale === 'pt' ? 'PT | EN' : 'EN | PT' }}
        </button>
      </div>
    </header>

    <main class="layout">
      <section class="hero card">
        <p class="tag">Software Engineer + Applied AI</p>
        <h1>{{ t.heroTitle }}</h1>
        <p class="subtitle">
          {{ t.heroSubtitle1 }}
          {{ t.heroSubtitle2 }}
        </p>
        <div class="hero-actions">
          <a class="btn btn-primary" href="#focus">{{ t.heroCta }}</a>
          <a class="btn btn-ghost" href="https://github.com/ygarasab" target="_blank" rel="noopener noreferrer">GitHub</a>
        </div>
      </section>

      <section id="about" class="card">
        <h2>{{ t.aboutTitle }}</h2>
        <p>
          {{ t.aboutTextBefore }} <strong>PHP e Laravel</strong> {{ t.aboutTextMiddle1 }}
          <strong>React e Vue</strong> {{ t.aboutTextMiddle2 }}
          <strong>Python</strong> {{ t.aboutTextAfter }}
        </p>
        <div class="chips">
          <span>PHP</span>
          <span>Laravel</span>
          <span>React</span>
          <span>Vue</span>
          <span>Python</span>
          <span>Machine Learning</span>
        </div>
      </section>

      <section id="focus" class="card spotlight">
        <h2>{{ t.focusTitle }}</h2>
        <p class="spotlight-title">{{ t.focusHeadline }}</p>
        <p>
          {{ t.focusDescription }}
        </p>
        <ul>
          <li>{{ t.focusItem1 }}</li>
          <li>{{ t.focusItem2 }}</li>
          <li>{{ t.focusItem3 }}</li>
        </ul>
      </section>

      <section id="projects" class="card">
        <h2>{{ t.projectsTitle }}</h2>
        <div class="project-grid">
          <article class="project">
            <h3>Computer Vision Research</h3>
            <p>{{ t.project1 }}</p>
          </article>
          <article class="project">
            <h3>Web Systems</h3>
            <p>{{ t.project2 }}</p>
          </article>
          <article class="project">
            <h3>Data + ML Pipelines</h3>
            <p>{{ t.project3 }}</p>
          </article>
        </div>
      </section>
    </main>

    <footer id="contact" class="footer">
      <p>{{ t.footerText }}</p>
      <div class="footer-links">
        <a href="https://www.ygarasab.com" target="_blank" rel="noopener noreferrer">Website</a>
        <a href="https://github.com/ygarasab" target="_blank" rel="noopener noreferrer">GitHub</a>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      locale: 'pt',
      messages: {
        pt: {
          navAbout: 'Sobre',
          navFocus: 'Foco',
          navProjects: 'Projetos',
          navContact: 'Contato',
          heroTitle: 'Construindo software com direção e pesquisa aplicada.',
          heroSubtitle1: 'Backend, frontend e dados conectados em produtos reais.',
          heroSubtitle2: 'Hoje, foco em visão computacional para agricultura.',
          heroCta: 'Ver foco atual',
          aboutTitle: 'Experiência abrangente',
          aboutTextBefore: 'Atuo com',
          aboutTextMiddle1: 'em APIs e regras de negócio,',
          aboutTextMiddle2: 'para interfaces web, e',
          aboutTextAfter: 'para automações, dados e machine learning.',
          focusTitle: 'Projeto de mestrado',
          focusHeadline: 'Identificação de estresse hídrico em plantas via vídeo',
          focusDescription: 'Pipeline em desenvolvimento com extração de frequência modal, processamento de sinais, engenharia de atributos e modelagem preditiva para detectar sinais de estresse.',
          focusItem1: 'Entrada: vídeos de plantas em diferentes condições hídricas',
          focusItem2: 'Sinal: frequência modal e variações ao longo do tempo',
          focusItem3: 'Saída: classificação e suporte à decisão para monitoramento',
          projectsTitle: 'Projetos atuais',
          project1: 'Experimentos para detecção de estresse hídrico com base em dinâmica modal de plantas.',
          project2: 'Aplicações e APIs com foco em clareza, arquitetura e evolução contínua.',
          project3: 'Fluxos de dados, validação de features e ciclos de treino para problemas aplicados.',
          footerText: 'Vamos construir algo útil.'
        },
        en: {
          navAbout: 'About',
          navFocus: 'Focus',
          navProjects: 'Projects',
          navContact: 'Contact',
          heroTitle: 'Building software with direction and applied research.',
          heroSubtitle1: 'Backend, frontend, and data connected in real products.',
          heroSubtitle2: 'Right now, my focus is computer vision for agriculture.',
          heroCta: 'See current focus',
          aboutTitle: 'Broad experience',
          aboutTextBefore: 'I work with',
          aboutTextMiddle1: 'on APIs and business rules,',
          aboutTextMiddle2: 'for web interfaces, and',
          aboutTextAfter: 'for automation, data, and machine learning.',
          focusTitle: "Master's project",
          focusHeadline: 'Water stress identification in plants through video',
          focusDescription: 'An evolving pipeline with modal frequency extraction, signal processing, feature engineering, and predictive modeling to detect stress signals.',
          focusItem1: 'Input: plant videos under different water conditions',
          focusItem2: 'Signal: modal frequency and temporal variations',
          focusItem3: 'Output: classification and decision support for monitoring',
          projectsTitle: 'Current projects',
          project1: 'Experiments for water stress detection based on plant modal dynamics.',
          project2: 'Applications and APIs focused on clarity, architecture, and continuous evolution.',
          project3: 'Data flows, feature validation, and training cycles for applied problems.',
          footerText: "Let's build something useful."
        }
      }
    }
  },
  computed: {
    t() {
      return this.messages[this.locale]
    }
  },
  methods: {
    toggleLocale() {
      this.locale = this.locale === 'pt' ? 'en' : 'pt'
    }
  }
}
</script>

<style scoped>
.page {
  min-height: 100vh;
  padding: 1.5rem;
  position: relative;
  z-index: 1;
  max-width: 1100px;
  margin: 0 auto;
}

.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.topbar-right {
  display: flex;
  align-items: center;
  gap: 0.7rem;
  flex-wrap: wrap;
  justify-content: flex-end;
}

.brand {
  font-size: 1rem;
  letter-spacing: 0.2rem;
  color: #00ff88;
  text-shadow: 0 0 10px rgba(0, 255, 136, 0.7);
}

.menu {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.menu a {
  color: #00ffff;
  text-decoration: none;
  border: 1px solid rgba(0, 255, 255, 0.4);
  padding: 0.35rem 0.7rem;
  border-radius: 999px;
  transition: 0.2s ease;
}

.menu a:hover {
  border-color: #00ff88;
  color: #00ff88;
}

.lang-switch {
  border: 1px solid rgba(0, 255, 136, 0.7);
  color: #00ff88;
  background: rgba(0, 0, 0, 0.35);
  padding: 0.35rem 0.6rem;
  border-radius: 999px;
  cursor: pointer;
  font-family: inherit;
}

.lang-switch:hover {
  box-shadow: 0 0 10px rgba(0, 255, 136, 0.35);
}

.layout {
  display: grid;
  gap: 1.1rem;
}

.card {
  background: rgba(8, 12, 20, 0.66);
  border: 1px solid rgba(0, 255, 255, 0.35);
  border-radius: 14px;
  padding: 1.3rem;
  backdrop-filter: blur(8px);
  box-shadow: inset 0 0 20px rgba(0, 255, 255, 0.06);
}

.hero h1 {
  font-size: clamp(1.7rem, 4vw, 2.6rem);
  color: #e5ffff;
  margin: 0.4rem 0 0.8rem;
}

.tag {
  color: #00ff88;
  letter-spacing: 0.08rem;
}

.subtitle {
  max-width: 70ch;
}

.hero-actions {
  margin-top: 1rem;
  display: flex;
  gap: 0.7rem;
  flex-wrap: wrap;
}

.btn {
  text-decoration: none;
  padding: 0.6rem 0.9rem;
  border-radius: 8px;
  border: 1px solid #00ffff;
  color: #00ffff;
}

.btn-primary {
  border-color: #00ff88;
  color: #00ff88;
}

.btn-primary:hover,
.btn-ghost:hover {
  box-shadow: 0 0 16px rgba(0, 255, 255, 0.3);
}

.chips {
  margin-top: 0.9rem;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.chips span {
  border: 1px solid rgba(0, 255, 255, 0.35);
  border-radius: 999px;
  padding: 0.25rem 0.55rem;
  font-size: 0.85rem;
}

.spotlight {
  border-color: rgba(0, 255, 136, 0.45);
}

.spotlight-title {
  color: #00ff88;
  margin-bottom: 0.6rem;
}

.spotlight ul {
  margin-top: 0.8rem;
  padding-left: 1rem;
}

.spotlight li {
  margin: 0.35rem 0;
}

.project-grid {
  margin-top: 0.8rem;
  display: grid;
  gap: 0.8rem;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
}

.project {
  border: 1px solid rgba(0, 255, 255, 0.25);
  border-radius: 10px;
  padding: 0.9rem;
  background: rgba(0, 0, 0, 0.2);
}

.project h3 {
  margin-bottom: 0.45rem;
  color: #00ffff;
}

.footer {
  margin: 1.2rem 0 0.5rem;
  padding: 0.8rem 0.2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 0.8rem;
  flex-wrap: wrap;
}

.footer-links {
  display: flex;
  gap: 0.8rem;
}

.footer a {
  color: #00ffff;
}

@media (max-width: 768px) {
  .page {
    padding: 1rem;
  }

  .topbar {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
