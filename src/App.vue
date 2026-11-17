<script setup>
import NavBar from './components/NavBar.vue'
import Hero from './components/Hero.vue'
import About from './components/About.vue'
import Experience from './components/Experience.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Learning from './components/Learning.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="app">
    <div class="page-bg" aria-hidden="true"></div>

    <NavBar />
    <main>
      <Hero />
      <About />
      <Experience />
      <Projects />
      <Skills />
      <Learning />
    </main>
    <Footer />
  </div>
</template>

<style scoped>
.app {
  position: relative;
}

main {
  padding-top: var(--nav-height);
  position: relative;
  z-index: 1;
}

:deep(header) {
  z-index: 100;
}

.page-bg {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 0;
  background:
    linear-gradient(115deg, transparent 0 18%, rgba(45, 212, 191, 0.065) 18% 18.3%, transparent 18.3% 48%, rgba(167, 139, 250, 0.06) 48% 48.25%, transparent 48.25%),
    linear-gradient(180deg, rgba(45, 212, 191, 0.08), transparent 34%, rgba(167, 139, 250, 0.055) 74%, transparent);
  opacity: 0.9;
}
</style>
