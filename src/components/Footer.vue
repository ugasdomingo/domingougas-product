<script setup>
import { personalInfo } from '../data/portfolio.js'

const year = new Date().getFullYear()
</script>

<template>
  <footer class="footer">
    <hr class="separator" />
    <div class="container footer-inner">
      <p class="footer-copy">
        Diseñado y desarrollado por
        <a :href="personalInfo.github" target="_blank" rel="noopener noreferrer">
          Domingo Ugas
        </a>
        · {{ year }}
      </p>

      <div class="footer-socials">
        <a :href="`mailto:${personalInfo.email}`" class="social-link">
          Email
        </a>
        <a :href="personalInfo.github" target="_blank" rel="noopener noreferrer" class="social-link">
          GitHub
        </a>
        <a :href="personalInfo.linkedin" target="_blank" rel="noopener noreferrer" class="social-link">
          LinkedIn
        </a>
        <a :href="personalInfo.twitter" target="_blank" rel="noopener noreferrer" class="social-link">
          X
        </a>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  padding: 2rem 0 2.5rem;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding-top: 1.5rem;
}

.footer-copy {
  font-size: 0.875rem;
  color: var(--text-muted);
}

.footer-copy a,
.social-link {
  color: var(--text-secondary);
  transition: color 0.2s;
}

.footer-copy a:hover,
.social-link:hover {
  color: var(--accent-3);
}

.footer-socials {
  display: flex;
  gap: 0.9rem;
  align-items: center;
  font-size: 0.86rem;
  font-weight: 750;
}

@media (max-width: 500px) {
  .footer-inner {
    flex-direction: column;
    text-align: center;
  }
}
</style>
