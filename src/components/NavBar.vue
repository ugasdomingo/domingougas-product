<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { cvFiles, skillsTitle } from '../data/portfolio.js'

const mainCv = cvFiles.find(cv => cv.primary)

const scrolled = ref(false)

function handleScroll() {
  scrolled.value = window.scrollY > 20
}

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<template>
  <header :class="['navbar', { 'navbar--scrolled': scrolled }]">
    <div class="container nav-inner">
      <a href="#inicio" class="logo" aria-label="Ir al inicio">
        <img src="/logo.png" alt="Domingo Ugas" class="logo-img" />
        <span>Domingo Ugas</span>
      </a>

      <nav class="nav-links" aria-label="Navegación principal">
        <a href="#sobre-mi" class="nav-link">Sobre mí</a>
        <a href="#experiencia" class="nav-link">Experiencia</a>
        <a href="#proyectos" class="nav-link">Proyectos</a>
        <a href="#competencias" class="nav-link">{{ skillsTitle }}</a>
        <a href="#formacion" class="nav-link">Formación</a>
      </nav>

      <a
        :href="mainCv.href"
        target="_blank"
        rel="noopener"
        class="btn btn-primary github-btn"
        aria-label="Ver el CV de Domingo Ugas en PDF"
      >
        Ver CV
      </a>
    </div>
  </header>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  height: var(--nav-height);
  border-bottom: 1px solid transparent;
  transition: background 0.3s, border-color 0.3s, backdrop-filter 0.3s;
}

.navbar--scrolled {
  background: rgba(7, 7, 8, 0.78);
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);
  border-bottom-color: var(--border);
}

.nav-inner {
  height: 100%;
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.logo {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  gap: 0.65rem;
  font-size: 0.92rem;
  font-weight: 800;
}

.logo-img {
  height: 2.2rem;
  width: 2.2rem;
  border-radius: 50%;
  object-fit: cover;
  border: 1px solid rgba(255, 255, 255, 0.16);
  display: block;
}

.nav-links {
  display: flex;
  justify-content: center;
  gap: 0.125rem;
  flex: 1;
}

.nav-link {
  padding: 0.42rem 0.75rem;
  font-size: 0.86rem;
  color: var(--text-muted);
  border-radius: 0.45rem;
  transition: color 0.2s, background 0.2s;
}

.nav-link:hover {
  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.06);
}

.github-btn {
  flex-shrink: 0;
  min-height: 2.25rem;
  font-size: 0.82rem;
  padding: 0.55rem 0.85rem;
}

@media (max-width: 760px) {
  .nav-links {
    display: none;
  }

  .nav-inner {
    justify-content: space-between;
  }
}

@media (max-width: 420px) {
  .logo span {
    display: none;
  }
}
</style>
