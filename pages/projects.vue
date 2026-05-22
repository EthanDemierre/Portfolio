<template>
  <page-nav />

  <main class="page-main">
    <section class="projects-content">
      <div class="projects-header">
        <h2>Projets</h2>
      </div>
      
      <div class="projects-grid">
        <!-- Projects will be added here -->
      </div>
    </section>
  </main>
</template>

<style scoped>
.page-main {
  position: relative;
  z-index: 20;
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  padding: 2rem;
  border: 1rem solid var(--blue);
  pointer-events: none;
}

.page-main > * {
  pointer-events: auto;
}

@media (max-width: 1440px) {
  .page-main {
    padding: 1.75rem;
    border-width: 0.9rem;
  }
}

@media (max-width: 1024px) {
  .page-main {
    padding: 1.5rem;
    border-width: 0.75rem;
  }
}

@media (max-width: 768px) {
  .page-main {
    padding: 1rem;
    border-width: 0.5rem;
  }
}

@media (max-width: 480px) {
  .page-main {
    padding: 0.75rem;
    border-width: 0.35rem;
  }
}

.projects-content {
  grid-column: 2 / span 10;
  grid-row: 3 / span 8;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  pointer-events: auto;
}

@media (max-width: 1024px) {
  .projects-content {
    grid-column: 2 / span 10;
    grid-row: 3 / span 8;
  }
}

@media (max-width: 768px) {
  .projects-content {
    grid-column: 1 / span 12;
    grid-row: 2 / span 10;
  }
}

@media (max-width: 480px) {
  .projects-content {
    grid-column: 1 / -1;
    grid-row: 2 / span 10;
    padding: 1rem;
  }
}

.projects-header {
  width: 100%;
  text-align: center;
}

.projects-grid {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
  }
}

@media (max-width: 480px) {
  .projects-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }
}
</style>
