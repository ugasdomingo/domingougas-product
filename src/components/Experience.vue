<script setup>
import { experience } from '../data/portfolio.js'
</script>

<template>
  <section id="experiencia" class="experience">
    <div class="container">
      <h2 class="section-title">Experiencia</h2>

      <ol class="timeline">
        <li
          v-for="job in experience"
          :key="`${job.company}-${job.period}`"
          :class="['timeline-item', { 'timeline-item--current': job.current }]"
        >
          <span class="timeline-dot" aria-hidden="true"></span>

          <div class="job card">
            <div class="job-head">
              <div>
                <h3 class="job-role">{{ job.role }}</h3>
                <p class="job-company">
                  <a v-if="job.url" :href="job.url" target="_blank" rel="noopener noreferrer">{{ job.company }}</a>
                  <span v-else>{{ job.company }}</span>
                  <span v-if="job.context" class="job-context"> · {{ job.context }}</span>
                </p>
              </div>
              <span class="job-period">{{ job.period }}</span>
            </div>

            <ul class="job-bullets">
              <li v-for="(bullet, i) in job.bullets" :key="i">{{ bullet }}</li>
            </ul>

            <div v-if="job.projects" class="subprojects">
              <div v-for="project in job.projects" :key="project.name" class="subproject">
                <div class="subproject-head">
                  <a
                    v-if="project.url"
                    :href="project.url"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="subproject-name"
                  >{{ project.name }} ↗</a>
                  <span v-else class="subproject-name">{{ project.name }}</span>
                  <span class="subproject-period">{{ project.period }}</span>
                </div>
                <ul class="job-bullets">
                  <li v-for="(bullet, i) in project.bullets" :key="i">{{ bullet }}</li>
                </ul>
              </div>
            </div>
          </div>
        </li>
      </ol>
    </div>
  </section>
</template>

<style scoped>
.timeline {
  list-style: none;
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  padding-left: 1.75rem;
}

.timeline::before {
  content: '';
  position: absolute;
  top: 0.6rem;
  bottom: 0.6rem;
  left: 0.42rem;
  width: 1px;
  background: linear-gradient(180deg, rgba(45, 212, 191, 0.6), rgba(255, 255, 255, 0.08));
}

.timeline-item {
  position: relative;
}

.timeline-dot {
  position: absolute;
  left: -1.75rem;
  top: 1.45rem;
  width: 0.85rem;
  height: 0.85rem;
  border-radius: 50%;
  background: var(--bg-secondary);
  border: 2px solid var(--border-hover);
}

.timeline-item--current .timeline-dot {
  background: var(--accent-3);
  border-color: var(--accent-3);
  box-shadow: 0 0 0 5px rgba(45, 212, 191, 0.12);
}

.job {
  padding: 1.35rem 1.5rem;
}

.timeline-item--current .job {
  border-color: rgba(45, 212, 191, 0.26);
}

.job-head {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 0.8rem;
}

.job-role {
  font-size: 1.1rem;
  font-weight: 850;
  line-height: 1.3;
}

.job-company {
  margin-top: 0.2rem;
  font-size: 0.92rem;
  color: var(--accent-3);
  font-weight: 700;
}

.job-company a:hover {
  text-decoration: underline;
}

.job-context {
  color: var(--text-muted);
  font-weight: 500;
}

.job-period {
  flex-shrink: 0;
  padding: 0.25rem 0.7rem;
  border-radius: 999px;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.04);
  color: var(--text-secondary);
  font-size: 0.76rem;
  font-weight: 700;
  white-space: nowrap;
}

.job-bullets {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  padding-left: 1.1rem;
  color: var(--text-secondary);
  font-size: 0.9rem;
  line-height: 1.65;
}

.job-bullets li::marker {
  color: var(--accent-3);
}

.subprojects {
  margin-top: 1.1rem;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 0.75rem;
}

.subproject {
  padding: 1rem;
  border-radius: 0.6rem;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.025);
}

.subproject-head {
  display: flex;
  flex-direction: column;
  gap: 0.15rem;
  margin-bottom: 0.55rem;
}

.subproject-name {
  font-size: 0.92rem;
  font-weight: 800;
  color: var(--text-primary);
}

a.subproject-name:hover {
  color: var(--accent-3);
}

.subproject-period {
  font-size: 0.74rem;
  color: var(--text-muted);
}

.subproject .job-bullets {
  font-size: 0.84rem;
}

@media (max-width: 900px) {
  .subprojects {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 600px) {
  .timeline {
    padding-left: 1.25rem;
  }

  .timeline-dot {
    left: -1.25rem;
  }

  .timeline::before {
    left: 0.17rem;
  }

  .job {
    padding: 1.1rem;
  }

  .job-head {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>
