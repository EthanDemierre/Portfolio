<template>
  <page-nav />

  <main class="page-main">
    <section class="about-content">
      <div class="about-container">
        <h2>À propos</h2>
        <div class="about-squares">
          <svg xmlns="http://www.w3.org/2000/svg" width="68" height="68" viewBox="0 0 68 68" fill="none">
            <rect width="68" height="68" fill="#2600FF"/>
          </svg>
          <svg xmlns="http://www.w3.org/2000/svg" width="68" height="68" viewBox="0 0 68 68" fill="none">
            <rect width="68" height="68" fill="#FF0000"/>
          </svg>
        </div>

        <div class="about-text">
          <p>
            J'ai 21 ans et je viens de terminer mes études à l'ERACOM. Passionné par la création sous toutes ses formes,
            j'aime imaginer, construire, transformer des idées en expériences visuelles et interactives. Le mixmedia est pour moi un super moyen d'expression.
          </p>
          <p>
            Si je devais m'identifier à des couleurs je serais le rouge (<span class="red-text">FF0000</span>) et le bleu (<span class="blue-text">2600FF</span>)
            car...
          </p>
        </div>
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

.about-content {
  grid-column: 2 / span 10;
  grid-row: 3 / span 8;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  pointer-events: auto;
}

@media (max-width: 1440px) {
  .about-content {
    grid-column: 2 / span 10;
    grid-row: 3 / span 8;
  }
}

@media (max-width: 1024px) {
  .about-content {
    grid-column: 2 / span 10;
    grid-row: 3 / span 8;
  }
}

@media (max-width: 768px) {
  .about-content {
    grid-column: 1 / span 12;
    grid-row: 2 / span 10;
  }
}

@media (max-width: 480px) {
  .about-content {
    grid-column: 1 / -1;
    grid-row: 2 / span 10;
    padding: 1rem;
  }
}

.about-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
  text-align: center;
  width: 100%;
}

.about-squares {
  display: flex;
  gap: 3rem;
  justify-content: center;
  align-items: center;
}

@media (max-width: 768px) {
  .about-squares {
    gap: 2rem;
  }
}

@media (max-width: 480px) {
  .about-squares {
    gap: 1rem;
  }
}

.about-squares svg {
  width: 68px;
  height: 68px;
}

@media (max-width: 768px) {
  .about-squares svg {
    width: 50px;
    height: 50px;
  }
}

@media (max-width: 480px) {
  .about-squares svg {
    width: 40px;
    height: 40px;
  }
}

.about-text {
  max-width: 800px;
  text-align: left;
  font-family: monospace;
  line-height: 1.6;
}

.about-text p {
  margin-bottom: 1.5rem;
  font-size: 0.875rem;
}

@media (max-width: 768px) {
  .about-text p {
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .about-text p {
    font-size: 0.75rem;
    margin-bottom: 1rem;
  }
}

.red-text {
  color: red;
}

.blue-text {
  color: #2600FF;
}

h2 {
  width: 100%;
}
</style>
