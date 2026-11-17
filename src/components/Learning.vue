<script setup>
import { bootcampInfo, education } from '../data/portfolio.js'
</script>

<template>
  <section id="formacion" class="learning">
    <div class="container">
      <h2 class="section-title">Formación</h2>

      <div class="bootcamp-card card">
        <div class="bootcamp-copy">
          <div class="bootcamp-meta">
            <span class="live-badge">
              <span class="live-dot" aria-hidden="true"></span>
              Graduado
            </span>
            <span>{{ bootcampInfo.startDate }} · {{ bootcampInfo.endDate }}</span>
            <span>{{ bootcampInfo.duration }}</span>
          </div>
          <h3>{{ bootcampInfo.program }}</h3>
          <a :href="bootcampInfo.url" target="_blank" rel="noopener noreferrer">
            {{ bootcampInfo.school }}
          </a>
          <p class="bootcamp-summary">{{ bootcampInfo.summary }}</p>
        </div>

        <div class="bootcamp-signal" aria-hidden="true">
          <span style="--w: 62%"></span>
          <span style="--w: 82%"></span>
          <span style="--w: 48%"></span>
          <span style="--w: 74%"></span>
        </div>
      </div>

      <div class="edu-block">
        <h3 class="block-heading">Trayectoria formativa</h3>

        <div class="edu-list">
          <div
            v-for="(edu, i) in education"
            :key="i"
            :class="['edu-item card', { 'edu-item--current': edu.status === 'current' }]"
          >
            <div class="edu-left">
              <div class="edu-type-badge" :class="edu.status === 'current' ? 'badge--current' : 'badge--done'">
                {{ edu.type }}
              </div>
              <div class="edu-period">{{ edu.period }}</div>
            </div>

            <div class="edu-body">
              <div class="edu-title-row">
                <h4>{{ edu.title }}</h4>
                <a v-if="edu.url" :href="edu.url" target="_blank" rel="noopener noreferrer">
                  {{ edu.school }}
                </a>
                <span v-else>{{ edu.school }}</span>
              </div>
              <p>{{ edu.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.bootcamp-card {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 340px;
  gap: 2rem;
  padding: 1.6rem;
  margin-bottom: 3rem;
  border-color: rgba(45, 212, 191, 0.28);
  background:
    linear-gradient(145deg, rgba(45, 212, 191, 0.12), transparent 44%),
    var(--bg-card);
}

.bootcamp-meta {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.65rem;
  margin-bottom: 0.75rem;
  color: var(--text-muted);
  font-size: 0.82rem;
}

.live-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  color: #4ade80;
  background: rgba(34, 197, 94, 0.1);
  border: 1px solid rgba(34, 197, 94, 0.25);
  padding: 0.18rem 0.6rem;
  border-radius: 9999px;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.07em;
}

.live-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #4ade80;
  animation: pulse-dot 1.8s ease-in-out infinite;
}

@keyframes pulse-dot {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.45; transform: scale(0.68); }
}

.bootcamp-card h3 {
  font-size: clamp(1.5rem, 3vw, 2.45rem);
  line-height: 1.05;
  margin-bottom: 0.7rem;
}

.bootcamp-card a {
  color: var(--accent-3);
  font-weight: 750;
}

.bootcamp-summary {
  margin-top: 0.8rem;
  color: var(--text-muted);
  line-height: 1.7;
  max-width: 560px;
}

.bootcamp-signal {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.75rem;
}

.bootcamp-signal span {
  display: block;
  width: var(--w);
  height: 0.72rem;
  border-radius: 999px;
  background: linear-gradient(90deg, #2dd4bf, #a78bfa);
  box-shadow: 0 0 22px rgba(45, 212, 191, 0.16);
}

.block-intro {
  display: grid;
  grid-template-columns: 0.58fr 1fr;
  gap: 2rem;
  margin-bottom: 1.4rem;
}

.block-intro h3,
.block-heading {
  font-size: 1.2rem;
  font-weight: 850;
  color: var(--text-primary);
}

.block-intro p {
  color: var(--text-muted);
  line-height: 1.75;
}

.competencies-block,
.edu-block {
  margin-bottom: 3.5rem;
}

.competencies-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.9rem;
}

.comp-card {
  min-height: 14rem;
  padding: 1.2rem;
}

.comp-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 2rem;
  min-width: 2.7rem;
  padding: 0 0.55rem;
  border-radius: 0.55rem;
  background: rgba(45, 212, 191, 0.12);
  color: var(--accent-3);
  font-size: 0.68rem;
  font-weight: 900;
  margin-bottom: 1rem;
}

.comp-card h4 {
  font-size: 0.98rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
}

.comp-card p {
  color: var(--text-muted);
  font-size: 0.82rem;
  line-height: 1.65;
}

.edu-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-top: 1rem;
}

.edu-item {
  display: grid;
  grid-template-columns: 180px 1fr;
  gap: 1.5rem;
  padding: 1.25rem 1.5rem;
}

.edu-item--current {
  border-color: rgba(45, 212, 191, 0.25);
}

.edu-left {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.edu-type-badge {
  display: inline-block;
  width: fit-content;
  font-size: 0.68rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  padding: 0.18rem 0.55rem;
  border-radius: 999px;
}

.badge--current {
  background: var(--accent-dim);
  color: var(--accent-3);
  border: 1px solid rgba(45, 212, 191, 0.25);
}

.badge--done {
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-muted);
  border: 1px solid var(--border);
}

.edu-period,
.edu-body p,
.edu-title-row span {
  color: var(--text-muted);
}

.edu-period {
  font-size: 0.8rem;
}

.edu-title-row {
  display: flex;
  align-items: baseline;
  gap: 0.75rem;
  flex-wrap: wrap;
  margin-bottom: 0.35rem;
}

.edu-title-row h4 {
  font-size: 1rem;
  font-weight: 800;
}

.edu-title-row a {
  color: var(--accent-3);
  font-size: 0.84rem;
  font-weight: 750;
}

.edu-body p {
  font-size: 0.88rem;
  line-height: 1.65;
}

@media (max-width: 1024px) {
  .competencies-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 760px) {
  .bootcamp-card,
  .block-intro,
  .edu-item {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 560px) {
  .competencies-grid {
    grid-template-columns: 1fr;
  }
}
</style>
