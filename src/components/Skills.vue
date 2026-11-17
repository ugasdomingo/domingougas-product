<script setup>
import { skills, skillsTitle } from '../data/portfolio.js'
</script>

<template>
  <section id="competencias" class="skills">
    <div class="container">
      <h2 class="section-title">{{ skillsTitle }}</h2>

      <div class="skills-grid">
        <div
          v-for="group in skills"
          :key="group.label"
          :class="['skill-group card', { 'skill-group--learning': group.accent, 'skill-group--ai': group.ai, 'skill-group--wide': group.wide }]"
        >
          <div class="group-header">
            <span class="group-icon" aria-hidden="true">{{ group.icon }}</span>
            <div>
              <h3 class="group-label">{{ group.label }}</h3>
              <p v-if="group.note" class="group-note">{{ group.note }}</p>
            </div>
          </div>

          <div class="tags-row">
            <span
              v-for="skill in group.items"
              :key="skill"
              :class="['tag', group.ai ? 'tag-violet' : group.accent ? 'tag-accent' : 'tag-default']"
            >
              {{ skill }}
            </span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
}

.skill-group {
  position: relative;
  min-height: 18rem;
  padding: 1.35rem;
  overflow: hidden;
}

.skill-group::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.055), transparent 38%);
  pointer-events: none;
}

.skill-group--learning {
  border-color: rgba(45, 212, 191, 0.28);
  background:
    linear-gradient(160deg, rgba(45, 212, 191, 0.12), transparent 45%),
    var(--bg-card);
}

.skill-group--ai {
  border-color: rgba(167, 139, 250, 0.3);
  background:
    linear-gradient(160deg, rgba(167, 139, 250, 0.12), transparent 45%),
    var(--bg-card);
}

.skill-group--wide {
  grid-column: 1 / -1;
  min-height: auto;
}

.group-header {
  position: relative;
  display: flex;
  align-items: flex-start;
  gap: 0.8rem;
  margin-bottom: 1.25rem;
}

.group-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 0.65rem;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.045);
  color: var(--accent-3);
  font-size: 0.72rem;
  font-weight: 900;
}

.group-label {
  font-size: 1.05rem;
  font-weight: 800;
  color: var(--text-primary);
  line-height: 1.1;
}

.group-note {
  margin-top: 0.28rem;
  font-size: 0.76rem;
  color: var(--text-muted);
}

.tags-row {
  position: relative;
  display: flex;
  flex-wrap: wrap;
  gap: 0.45rem;
}

@media (max-width: 1020px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }

  .skill-group {
    min-height: auto;
  }
}
</style>
