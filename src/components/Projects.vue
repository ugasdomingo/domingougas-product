<script setup>
import { ref, computed, onMounted } from 'vue'
import { projects, recentSites } from '../data/portfolio.js'

onMounted(() => {
  document.querySelectorAll('.site-img').forEach(img => {
    if (img.complete && img.naturalWidth > 0) img.classList.add('loaded')
  })
})

const filters = [
  { key: 'all', label: 'Todos' },
  { key: 'producto', label: 'Productos' },
  { key: 'client', label: 'Webs para clientes' },
  { key: 'datascience', label: 'Data Science' },
]

const categoryLabel = {
  producto: 'Producto',
  client: 'Web corporativa',
  datascience: 'Data Science',
}

const activeFilter = ref('all')

const filtered = computed(() =>
  activeFilter.value === 'all'
    ? projects
    : projects.filter(p => p.category === activeFilter.value)
)
</script>

<template>
  <section id="proyectos" class="projects">
    <div class="container">
      <h2 class="section-title">Proyectos</h2>

      <div class="recent-block">
        <div class="recent-intro">
          <span class="tag tag-accent">En producción</span>
          <h3>Productos con resultados medibles</h3>
        </div>

        <div class="recent-grid">
          <a
            v-for="site in recentSites"
            :key="site.url"
            :href="site.url"
            target="_blank"
            rel="noopener noreferrer"
            class="site-card"
            :aria-label="`Visitar ${site.name}`"
          >
            <div class="site-img-wrap">
              <div class="site-skeleton" aria-hidden="true"></div>
              <img
                :src="site.screenshot"
                :alt="`Captura de ${site.name}`"
                class="site-img"
                loading="lazy"
                @load="(e) => e.target.classList.add('loaded')"
              />
            </div>
            <div class="site-info">
              <span class="site-name">{{ site.name }}</span>
              <span class="site-desc">{{ site.description }}</span>
            </div>
          </a>
        </div>
      </div>

      <div class="filter-tabs" role="tablist" aria-label="Filtrar proyectos">
        <button
          v-for="f in filters"
          :key="f.key"
          :class="['filter-btn', { active: activeFilter === f.key }]"
          role="tab"
          :aria-selected="activeFilter === f.key"
          @click="activeFilter = f.key"
        >
          {{ f.label }}
        </button>
      </div>

      <div class="projects-grid">
        <article
          v-for="project in filtered"
          :key="project.id"
          :class="['project-card card', { 'project-card--featured': project.featured }]"
        >
          <div class="card-header">
            <div>
              <span class="project-category">{{ categoryLabel[project.category] }}</span>
              <h3 class="project-name">{{ project.name }}</h3>
            </div>
            <div class="card-links">
              <a
                v-if="project.github"
                :href="project.github"
                target="_blank"
                rel="noopener noreferrer"
                class="icon-link"
                :aria-label="`Código de ${project.name} en GitHub`"
                title="Ver en GitHub"
              >
                GH
              </a>
              <a
                v-if="project.url"
                :href="project.url"
                target="_blank"
                rel="noopener noreferrer"
                class="icon-link"
                :aria-label="`Ver demo de ${project.name}`"
                title="Ver demo"
              >
                ↗
              </a>
            </div>
          </div>

          <p class="project-desc">{{ project.description }}</p>

          <div class="project-tags">
            <span v-for="tag in project.tags" :key="tag" class="tag tag-default">
              {{ tag }}
            </span>
          </div>

          <div v-if="project.featured" class="featured-pill" aria-label="Proyecto destacado">
            Destacado
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.recent-block {
  margin-bottom: 3.5rem;
}

.recent-intro {
  display: flex;
  justify-content: space-between;
  align-items: end;
  gap: 1rem;
  margin-bottom: 1rem;
}

.recent-intro h3 {
  max-width: 520px;
  font-size: clamp(1.3rem, 2.4vw, 2rem);
  line-height: 1.15;
  text-align: right;
}

.recent-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.site-card {
  display: flex;
  flex-direction: column;
  border-radius: 0.85rem;
  overflow: hidden;
  border: 1px solid var(--border);
  background: var(--bg-card);
  transition: border-color 0.25s, transform 0.25s, box-shadow 0.25s;
}

.site-card:hover {
  border-color: rgba(45, 212, 191, 0.38);
  transform: translateY(-5px);
  box-shadow: 0 18px 55px rgba(0, 0, 0, 0.42);
}

.site-img-wrap {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 10;
  overflow: hidden;
  background: var(--bg-secondary);
}

.site-skeleton {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, var(--bg-secondary) 25%, rgba(45, 212, 191, 0.08) 50%, var(--bg-secondary) 75%);
  background-size: 200% 100%;
  animation: shimmer 1.6s infinite;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}

.site-img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
  opacity: 0;
  transition: opacity 0.4s ease, transform 0.4s ease, filter 0.3s;
}

.site-img.loaded {
  opacity: 1;
}

.site-card:hover .site-img {
  transform: scale(1.04);
  filter: saturate(1.08) contrast(1.02);
}

.site-info {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  padding: 0.95rem 1rem;
}

.site-name {
  font-size: 0.98rem;
  font-weight: 800;
}

.site-desc {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.filter-tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.25rem;
}

.filter-btn {
  padding: 0.48rem 0.9rem;
  border-radius: 0.5rem;
  font-size: 0.82rem;
  font-weight: 750;
  cursor: pointer;
  transition: all 0.2s;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.035);
  color: var(--text-muted);
}

.filter-btn:hover {
  color: var(--text-secondary);
  border-color: var(--border-hover);
}

.filter-btn.active {
  background: var(--accent-3);
  color: #06100f;
  border-color: var(--accent-3);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}

.project-card {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1rem;
  min-height: 22rem;
  padding: 1.35rem;
  overflow: hidden;
}

.project-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 18px 55px rgba(0, 0, 0, 0.32);
}

.project-card--featured {
  border-color: rgba(45, 212, 191, 0.28);
}

.project-card--featured::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(145deg, rgba(45, 212, 191, 0.1), transparent 42%);
  pointer-events: none;
}

.card-header,
.project-desc,
.project-tags {
  position: relative;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 0.75rem;
}

.project-category {
  display: block;
  color: var(--accent-3);
  font-size: 0.68rem;
  text-transform: uppercase;
  font-weight: 900;
  letter-spacing: 0.09em;
  margin-bottom: 0.45rem;
}

.project-name {
  font-size: 1.15rem;
  font-weight: 850;
  line-height: 1.25;
}

.card-links {
  display: flex;
  gap: 0.35rem;
  flex-shrink: 0;
}

.icon-link {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  border-radius: 0.45rem;
  color: var(--text-secondary);
  background: rgba(255, 255, 255, 0.045);
  border: 1px solid var(--border);
  font-size: 0.72rem;
  font-weight: 900;
  transition: color 0.2s, background 0.2s, border-color 0.2s;
}

.icon-link:hover {
  color: var(--text-primary);
  background: rgba(255, 255, 255, 0.08);
  border-color: var(--border-hover);
}

.project-desc {
  font-size: 0.88rem;
  color: var(--text-muted);
  line-height: 1.72;
  flex: 1;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
  margin-top: auto;
}

.featured-pill {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(45, 212, 191, 0.13);
  color: var(--accent-3);
  border: 1px solid rgba(45, 212, 191, 0.28);
  font-size: 0.64rem;
  font-weight: 900;
  padding: 0.2rem 0.55rem;
  border-radius: 9999px;
  text-transform: uppercase;
  letter-spacing: 0.07em;
}

.project-card--featured .card-header {
  padding-right: 5.6rem;
}

@media (max-width: 1020px) {
  .projects-grid,
  .recent-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 680px) {
  .projects-grid,
  .recent-grid {
    grid-template-columns: 1fr;
  }

  .recent-intro {
    display: block;
  }

  .recent-intro h3 {
    margin-top: 0.8rem;
    text-align: left;
  }

  .project-card {
    min-height: auto;
  }
}
</style>
