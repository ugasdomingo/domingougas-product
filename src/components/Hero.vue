<script setup>
import { personalInfo, impactMetrics, neuralNodes, cvFiles, heroCopy } from '../data/portfolio.js'

const mainCv = cvFiles.find(cv => cv.primary)
</script>

<template>
  <section id="inicio" class="hero">
    <div class="container hero-content">
      <div class="hero-copy">
        <p class="eyebrow">
          <span class="status-dot" aria-hidden="true"></span>
          Disponible para trabajar · {{ personalInfo.location }}
        </p>

        <h1 class="hero-name">
          {{ personalInfo.name.split(' ')[0] }}
          <span>{{ personalInfo.name.split(' ')[1] }}</span>
        </h1>

        <p class="hero-role">
          <strong>{{ heroCopy.roleStrong }}</strong> {{ heroCopy.roleRest }}
        </p>

        <p class="hero-description">{{ heroCopy.description }}</p>

        <div class="hero-cta">
          <a :href="mainCv.href" target="_blank" rel="noopener" class="btn btn-primary">
            Ver CV
            <svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" aria-hidden="true">
              <path d="M12 4v12M6 10l6 6 6-6M5 20h14" />
            </svg>
          </a>

          <a href="#experiencia" class="btn btn-secondary">
            Ver experiencia
          </a>

          <a
            :href="personalInfo.linkedin"
            target="_blank"
            rel="noopener noreferrer"
            class="btn btn-secondary"
          >
            LinkedIn
          </a>
        </div>
      </div>

      <aside class="hero-lab" aria-label="Resumen visual del perfil">
        <div class="lab-topbar">
          <span></span>
          <span></span>
          <span></span>
          <p>domingougas.vercel.app</p>
        </div>

        <div class="lab-grid">
          <div class="terminal-panel">
            <p class="terminal-line muted">{{ heroCopy.command }}</p>
            <p class="terminal-line"><span>status</span> disponible para trabajar</p>
            <p class="terminal-line"><span>location</span> {{ personalInfo.location }}</p>
            <p class="terminal-line"><span>{{ heroCopy.focusKey }}</span> {{ heroCopy.focus }}</p>
          </div>

          <div class="model-panel">
            <div class="model-header">
              <span>conversión DigiNode</span>
              <strong>+20%</strong>
            </div>
            <div class="bars" aria-hidden="true">
              <span style="--h: 42%"></span>
              <span style="--h: 76%"></span>
              <span style="--h: 58%"></span>
              <span style="--h: 88%"></span>
              <span style="--h: 63%"></span>
              <span style="--h: 95%"></span>
            </div>
          </div>

          <div class="graph-panel">
            <svg class="graph-lines" viewBox="0 0 100 80" aria-hidden="true">
              <path d="M14 24 L41 17 L74 29 L84 57 L58 67 L24 62 Z" />
              <path d="M41 17 L58 67 M24 62 L74 29" />
            </svg>
            <span
              v-for="node in neuralNodes"
              :key="node.label"
              class="graph-node"
              :style="{ left: `${node.x}%`, top: `${node.y}%` }"
            >
              {{ node.label }}
            </span>
          </div>
        </div>
      </aside>
    </div>

    <div class="hero-metrics container" aria-label="Métricas clave">
      <div v-for="metric in impactMetrics" :key="metric.label" class="metric">
        <strong>{{ metric.value }}</strong>
        <span>{{ metric.label }}</span>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: calc(100vh - var(--nav-height));
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow: hidden;
  padding: 5rem 0 3rem;
}

.hero::before {
  content: '';
  position: absolute;
  inset: 5rem 0 auto;
  height: 42rem;
  background:
    linear-gradient(115deg, transparent 0 25%, rgba(45, 212, 191, 0.1) 25% 25.5%, transparent 25.5% 55%, rgba(99, 102, 241, 0.12) 55% 55.4%, transparent 55.4%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.035), transparent 65%);
  mask-image: linear-gradient(90deg, transparent, #000 18%, #000 82%, transparent);
  pointer-events: none;
}

.hero-content {
  display: grid;
  grid-template-columns: minmax(0, 0.9fr) minmax(340px, 1fr);
  align-items: center;
  gap: 3rem;
  position: relative;
  z-index: 1;
}

.hero-copy {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.55rem;
  padding: 0.42rem 0.75rem;
  border: 1px solid rgba(45, 212, 191, 0.28);
  border-radius: 999px;
  background: rgba(8, 47, 73, 0.36);
  color: var(--text-secondary);
  font-size: 0.82rem;
  margin-bottom: 1.35rem;
}

.status-dot {
  width: 0.48rem;
  height: 0.48rem;
  border-radius: 50%;
  background: var(--accent-3);
  box-shadow: 0 0 0 5px rgba(45, 212, 191, 0.1);
}

.hero-name {
  font-size: clamp(3.4rem, 9vw, 7rem);
  font-weight: 900;
  line-height: 0.86;
  letter-spacing: 0;
  margin-bottom: 1.5rem;
}

.hero-name span {
  display: block;
  color: transparent;
  -webkit-text-stroke: 1px rgba(250, 250, 250, 0.5);
  background: linear-gradient(135deg, #ffffff 8%, #2dd4bf 42%, #a78bfa 76%);
  -webkit-background-clip: text;
  background-clip: text;
}

.hero-role {
  font-size: clamp(1.35rem, 2vw, 1.9rem);
  line-height: 1.25;
  color: var(--text-primary);
  max-width: 650px;
  margin-bottom: 1rem;
}

.hero-role strong {
  color: var(--accent-3);
  font-weight: 800;
}

.hero-description {
  color: var(--text-muted);
  max-width: 590px;
  line-height: 1.8;
  margin-bottom: 2rem;
}

.hero-cta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.hero-lab {
  position: relative;
  min-height: 520px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  border-radius: 1rem;
  overflow: hidden;
  background:
    linear-gradient(145deg, rgba(24, 24, 27, 0.95), rgba(9, 9, 11, 0.8)),
    repeating-linear-gradient(90deg, rgba(255, 255, 255, 0.05) 0 1px, transparent 1px 52px),
    repeating-linear-gradient(0deg, rgba(255, 255, 255, 0.04) 0 1px, transparent 1px 52px);
  box-shadow: 0 24px 90px rgba(0, 0, 0, 0.55), inset 0 1px 0 rgba(255, 255, 255, 0.08);
}

.hero-lab::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, transparent, rgba(45, 212, 191, 0.12), transparent);
  transform: translateX(-80%);
  animation: scan 6s ease-in-out infinite;
}

@keyframes scan {
  0%, 30% { transform: translateX(-90%); }
  70%, 100% { transform: translateX(90%); }
}

.lab-topbar {
  height: 3rem;
  display: flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.09);
  color: var(--text-muted);
  font-size: 0.78rem;
}

.lab-topbar span {
  width: 0.65rem;
  height: 0.65rem;
  border-radius: 50%;
  background: var(--border-hover);
}

.lab-topbar span:nth-child(1) { background: #fb7185; }
.lab-topbar span:nth-child(2) { background: #facc15; }
.lab-topbar span:nth-child(3) { background: #34d399; }
.lab-topbar p { margin-left: auto; }

.lab-grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1fr 0.78fr;
  grid-template-rows: 180px 1fr;
  gap: 1rem;
  padding: 1rem;
  min-height: 470px;
}

.terminal-panel,
.model-panel,
.graph-panel {
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 0.75rem;
  background: rgba(9, 9, 11, 0.66);
  backdrop-filter: blur(12px);
}

.terminal-panel {
  grid-column: 1 / -1;
  padding: 1.2rem;
  font-family: 'SFMono-Regular', Consolas, monospace;
  overflow: hidden;
}

.terminal-line {
  color: var(--text-secondary);
  font-size: 0.88rem;
  line-height: 1.9;
  white-space: nowrap;
}

.terminal-line span {
  color: var(--accent-3);
  margin-right: 0.85rem;
}

.terminal-line.muted {
  color: var(--text-muted);
}

.model-panel {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.model-header {
  display: flex;
  justify-content: space-between;
  color: var(--text-muted);
  font-size: 0.76rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.model-header strong {
  color: var(--accent-3);
}

.bars {
  height: 170px;
  display: flex;
  align-items: flex-end;
  gap: 0.5rem;
}

.bars span {
  flex: 1;
  height: var(--h);
  border-radius: 0.4rem 0.4rem 0.1rem 0.1rem;
  background: linear-gradient(180deg, #a78bfa, #2dd4bf);
  box-shadow: 0 0 22px rgba(45, 212, 191, 0.18);
  animation: barPulse 3.4s ease-in-out infinite;
}

.bars span:nth-child(even) {
  animation-delay: 0.45s;
}

@keyframes barPulse {
  0%, 100% { transform: scaleY(0.9); opacity: 0.78; }
  50% { transform: scaleY(1); opacity: 1; }
}

.graph-panel {
  position: relative;
  min-height: 250px;
  overflow: hidden;
}

.graph-lines {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

.graph-lines path {
  fill: none;
  stroke: rgba(45, 212, 191, 0.52);
  stroke-width: 0.7;
  stroke-dasharray: 4 5;
  animation: dash 16s linear infinite;
}

@keyframes dash {
  to { stroke-dashoffset: -90; }
}

.graph-node {
  position: absolute;
  transform: translate(-50%, -50%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 3.4rem;
  height: 2rem;
  padding: 0 0.55rem;
  border-radius: 999px;
  border: 1px solid rgba(45, 212, 191, 0.34);
  background: rgba(15, 23, 42, 0.9);
  color: var(--text-primary);
  font-size: 0.72rem;
  font-weight: 700;
  box-shadow: 0 0 24px rgba(45, 212, 191, 0.12);
}

.hero-metrics {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.8rem;
  margin-top: 2.25rem;
}

.metric {
  min-height: 6rem;
  padding: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 0.8rem;
  background: rgba(24, 24, 27, 0.58);
}

.metric strong {
  display: block;
  font-size: 1.45rem;
  color: var(--text-primary);
  line-height: 1;
  margin-bottom: 0.5rem;
}

.metric span {
  color: var(--text-muted);
  font-size: 0.78rem;
  line-height: 1.4;
}

@media (max-width: 980px) {
  .hero-content {
    grid-template-columns: 1fr;
  }

  .hero-lab {
    min-height: 460px;
  }

  .hero-metrics {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .hero {
    padding-top: 3rem;
  }

  .hero-lab {
    min-height: auto;
  }

  .lab-grid {
    grid-template-columns: 1fr;
    grid-template-rows: auto;
    min-height: auto;
  }

  .graph-panel {
    min-height: 230px;
  }

  .hero-cta,
  .hero-cta .btn {
    width: 100%;
    justify-content: center;
  }

  .hero-metrics {
    grid-template-columns: 1fr;
  }
}
</style>
