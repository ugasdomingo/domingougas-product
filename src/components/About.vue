<script setup>
import { personalInfo, aboutLead, aboutParagraphs, aboutBadges, highlights, cvFiles } from '../data/portfolio.js'
</script>

<template>
  <section id="sobre-mi" class="about">
    <div class="container">
      <h2 class="section-title">¿Quién soy?</h2>

      <div class="about-grid">
        <div class="about-text">
          <p class="lead">{{ aboutLead }}</p>

          <p v-for="(paragraph, i) in aboutParagraphs" :key="i">{{ paragraph }}</p>

          <div class="about-badges">
            <span class="tag tag-accent">{{ personalInfo.location }}</span>
            <span class="tag tag-green">Disponible para trabajar</span>
            <span v-for="badge in aboutBadges" :key="badge" class="tag tag-default">{{ badge }}</span>
          </div>
        </div>

        <aside class="profile-card card" aria-label="Información personal">
          <img :src="personalInfo.photo" :alt="`Foto de ${personalInfo.name}`" class="profile-photo" />

          <dl class="profile-info">
            <div>
              <dt>Email</dt>
              <dd><a :href="`mailto:${personalInfo.email}`">{{ personalInfo.email }}</a></dd>
            </div>
            <div>
              <dt>LinkedIn</dt>
              <dd>
                <a :href="personalInfo.linkedin" target="_blank" rel="noopener noreferrer">
                  linkedin.com/in/ugasdomingo
                </a>
              </dd>
            </div>
            <div>
              <dt>GitHub</dt>
              <dd>
                <a :href="personalInfo.github" target="_blank" rel="noopener noreferrer">
                  github.com/ugasdomingo
                </a>
              </dd>
            </div>
          </dl>

          <div class="cv-downloads">
            <a
              v-for="cv in cvFiles"
              :key="cv.href"
              :href="cv.href"
              target="_blank"
              rel="noopener"
              :class="['btn', cv.primary ? 'btn-primary' : 'btn-secondary', 'cv-btn']"
            >
              <span class="cv-label">{{ cv.label }}</span>
              <span class="cv-note">{{ cv.note }}</span>
            </a>
          </div>
        </aside>
      </div>

      <div class="highlights-grid">
        <div v-for="item in highlights" :key="item.title" class="highlight card">
          <span class="highlight-icon" aria-hidden="true">{{ item.icon }}</span>
          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-grid {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 340px;
  gap: 3rem;
  align-items: start;
}

.about-text {
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
}

.about-text p {
  color: var(--text-secondary);
  line-height: 1.85;
  font-size: 1rem;
}

.about-text .lead {
  font-size: clamp(1.25rem, 2vw, 1.65rem);
  line-height: 1.45;
  color: var(--text-primary);
  font-weight: 650;
}

.about-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.profile-card {
  padding: 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 1.1rem;
  border-color: rgba(45, 212, 191, 0.22);
}

.profile-photo {
  width: 100%;
  aspect-ratio: 4 / 5;
  object-fit: cover;
  border-radius: 0.6rem;
  border: 1px solid var(--border);
  display: block;
}

.profile-info {
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
}

.profile-info dt {
  font-size: 0.68rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
}

.profile-info dd {
  font-size: 0.9rem;
  color: var(--text-secondary);
  overflow-wrap: anywhere;
}

.profile-info a:hover {
  color: var(--accent-3);
}

.cv-downloads {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.cv-btn {
  flex-direction: column;
  align-items: flex-start;
  gap: 0.3rem;
  width: 100%;
}

.cv-label {
  font-size: 0.92rem;
}

.cv-note {
  font-size: 0.74rem;
  font-weight: 500;
  opacity: 0.8;
}

.highlights-grid {
  margin-top: 2.5rem;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.highlight {
  padding: 1.35rem;
}

.highlight-icon {
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
  margin-bottom: 0.9rem;
}

.highlight h3 {
  font-size: 1.05rem;
  font-weight: 800;
  margin-bottom: 0.45rem;
}

.highlight p {
  color: var(--text-muted);
  font-size: 0.88rem;
  line-height: 1.7;
}

@media (max-width: 900px) {
  .about-grid {
    grid-template-columns: 1fr;
  }

  .profile-card {
    max-width: 420px;
  }

  .highlights-grid {
    grid-template-columns: 1fr;
  }
}
</style>
