<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]">
    <slider />
  </section>

  <main class="grid-container">
    <button ref="menuBtn" @click="toggleNav">
      <img src="public/img/menu.svg" alt="">
    </button>

    <div class="projects-scroll-container" @mouseenter="pauseScroll" @mouseleave="resumeScroll">
      <div class="projects-list" :style="{ transform: getLoopedTransform() }">
        <div v-for="(project, index) in projects" :key="index" class="project-item" @mouseenter="hoveredIndex = index" @mouseleave="hoveredIndex = -1">
          <div class="project-image-wrapper">
            <img :src="project.image" :alt="project.title" class="project-image" :class="{ blurred: hoveredIndex === index }" />
            <div v-if="hoveredIndex === index" class="project-info">
              <div class="project-info-content">
                <p class="project-date">{{ project.date }}</p>
                <p class="project-description">{{ project.description }}</p>
                <p class="project-medium">{{ project.medium }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      showNav: false,
      scrollPosition: 0,
      isScrolling: true,
      scrollSpeed: 3,
      hoveredIndex: -1,
      projects: []
    };
  },
  methods: {
    async loadProjects() {
      try {
        const response = await fetch('/api/projects');
        this.projects = await response.json();
      } catch (error) {
        console.error('Erreur lors du chargement des projets:', error);
      }
    },
    toggleNav() {
      this.showNav = !this.showNav;
    },
    handleClickOutside(event) {
      const nav = this.$refs.nav;
      const menuBtn = this.$refs.menuBtn;
      if (
        this.showNav &&
        nav &&
        !nav.contains(event.target) &&
        menuBtn &&
        !menuBtn.contains(event.target)
      ) {
        this.showNav = false;
      }
    },
    pauseScroll() {
      this.isScrolling = false;
    },
    resumeScroll() {
      this.isScrolling = true;
    },
    animateScroll() {
      if (this.isScrolling) {
        this.scrollPosition -= this.scrollSpeed;
      }
      requestAnimationFrame(this.animateScroll);
    },
    getLoopedTransform() {
      const itemHeight = 620;
      const totalHeight = this.projects.length * itemHeight;
      const position = ((this.scrollPosition % totalHeight) + totalHeight) % totalHeight;
      return `translateY(${-position}px)`;
    }
  },
  async mounted() {
    document.addEventListener('click', this.handleClickOutside);
    this.animateScroll();
    await this.loadProjects();
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClickOutside);
  }
};
</script>

<style scoped>
.navigation {
  position: absolute;
  z-index: 25;
  width: 25%;
  height: 100vh;
  background-color: var(--blue);
  box-shadow: 0 0px 10px rgb(0, 0, 0);
  transform: translateX(-100%);
  transition: transform 0.4s ease-in-out;
}

@media (max-width: 1440px) {
  .navigation {
    width: 30%;
  }
}

@media (max-width: 1024px) {
  .navigation {
    width: 40%;
  }
}

@media (max-width: 768px) {
  .navigation {
    width: 60%;
  }
}

@media (max-width: 480px) {
  .navigation {
    width: 100%;
  }
}

.navigation--active {
  transform: translateX(0);
}

button {
  background: none;
  border: none;
  position: absolute;
  top: 1rem;
  left: 1rem;
  z-index: 10;
  cursor: pointer;
}

.grid-container {
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  padding: 2rem;
  border: 1rem solid var(--blue);
  background-color: white;
  overflow: hidden;
}

@media (max-width: 1440px) {
  .grid-container {
    padding: 1.75rem;
    border-width: 0.9rem;
  }
}

@media (max-width: 1024px) {
  .grid-container {
    padding: 1.5rem;
    border-width: 0.75rem;
  }
}

@media (max-width: 768px) {
  .grid-container {
    padding: 1rem;
    border-width: 0.5rem;
  }
}

@media (max-width: 480px) {
  .grid-container {
    padding: 0.75rem;
    border-width: 0.35rem;
  }
}

.projects-scroll-container {
  grid-column: 1 / -1;
  grid-row: 1 / -1;
  width: 100%;
  height: 100%;
  overflow: hidden;
  position: relative;
  z-index: 5;
}

.projects-list {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  padding: 1rem;
  will-change: transform;
}

@media (max-width: 768px) {
  .projects-list {
    gap: 1.5rem;
    padding: 0.75rem;
  }
}

@media (max-width: 480px) {
  .projects-list {
    gap: 1rem;
    padding: 0.5rem;
  }
}

.project-item {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 600px;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.project-item:hover {
  transform: scale(1.02);
}

@media (max-width: 1024px) {
  .project-item {
    min-height: 450px;
  }
}

@media (max-width: 768px) {
  .project-item {
    min-height: 350px;
  }
}

@media (max-width: 480px) {
  .project-item {
    min-height: 250px;
  }
}

.project-image-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.project-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  border: 1px solid var(--black);
  transition: filter 0.3s ease;
}

.project-image.blurred {
  filter: blur(8px);
}

.project-info {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(255, 255, 255, 0.95);
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.project-info-content {
  text-align: center;
  padding: 2rem;
  width: 100%;
}

.project-date {
  font-family: 'Mono-light', sans-serif;
  font-size: 0.875rem;
  color: var(--black);
  margin-bottom: 1rem;
  letter-spacing: 0.0175rem;
}

.project-description {
  font-family: 'Mono-med', sans-serif;
  font-size: 1rem;
  color: var(--black);
  margin-bottom: 1.5rem;
  line-height: 1.5;
  font-weight: 300;
}

.project-medium {
  font-family: 'Mono-light-ita', sans-serif;
  font-size: 0.875rem;
  color: var(--black);
  font-style: italic;
  letter-spacing: 0.0175rem;
}

@media (max-width: 768px) {
  .project-info-content {
    padding: 1.5rem;
  }

  .project-date {
    font-size: 0.8rem;
  }

  .project-description {
    font-size: 0.9rem;
    margin-bottom: 1rem;
  }

  .project-medium {
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  .project-info-content {
    padding: 1rem;
  }

  .project-date {
    font-size: 0.75rem;
  }

  .project-description {
    font-size: 0.8rem;
    margin-bottom: 0.75rem;
  }

  .project-medium {
    font-size: 0.75rem;
  }
}
</style>
