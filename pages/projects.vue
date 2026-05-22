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

    <div class="projects-rain-container" @mouseenter="pauseRain" @mouseleave="resumeRain">
      <div
        v-for="(project, index) in animatedProjects"
        :key="`${project.id}-${index}`"
        class="project-rain-item"
        :style="getProjectStyle(index)"
      >
        <img :src="project.image" :alt="project.title" class="project-image" />
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      showNav: false,
      isRaining: true,
      projects: [
        { id: 1, title: 'Projet 1', image: '/img/projet/projet1.png' },
        { id: 2, title: 'Projet 2', image: '/img/projet/projet1.png' },
        { id: 3, title: 'Projet 3', image: '/img/projet/projet1.png' },
        { id: 4, title: 'Projet 4', image: '/img/projet/projet1.png' },
        { id: 5, title: 'Projet 5', image: '/img/projet/projet1.png' },
        { id: 6, title: 'Projet 6', image: '/img/projet/projet1.png' }
      ],
      animatedProjects: [],
      projectPositions: [],
      time: 0
    };
  },
  methods: {
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
    pauseRain() {
      this.isRaining = false;
    },
    resumeRain() {
      this.isRaining = true;
    },
    initializeRain() {
      this.animatedProjects = this.projects.concat(this.projects);
      this.projectPositions = this.animatedProjects.map(() => ({
        x: Math.random() * 80 + 10,
        startTime: Math.random() * 3000
      }));
    },
    getProjectStyle(index) {
      const duration = 15000;
      const containerHeight = window.innerHeight || 1000;
      
      const position = this.projectPositions[index];
      if (!position) return {};
      
      if (this.isRaining) {
        this.time += 16;
      }
      
      const elapsed = (this.time + position.startTime) % (duration + 1000);
      const progress = elapsed / (duration + 1000);
      const top = (progress * (containerHeight + 300)) - 300;
      
      return {
        left: `${position.x}%`,
        top: `${top}px`,
        opacity: progress < 0.1 ? progress * 10 : progress > 0.95 ? (1 - progress) * 20 : 1
      };
    },
    animate() {
      if (this.isRaining) {
        this.$forceUpdate();
      }
      requestAnimationFrame(this.animate);
    }
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
    this.initializeRain();
    this.animate();
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

.projects-rain-container {
  grid-column: 1 / -1;
  grid-row: 1 / -1;
  width: 100%;
  height: 100%;
  position: relative;
  z-index: 5;
  overflow: hidden;
}

.project-rain-item {
  position: absolute;
  width: 150px;
  height: 150px;
  display: flex;
  align-items: center;
  justify-content: center;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.1));
  will-change: transform, opacity;
}

@media (max-width: 1024px) {
  .project-rain-item {
    width: 120px;
    height: 120px;
  }
}

@media (max-width: 768px) {
  .project-rain-item {
    width: 100px;
    height: 100px;
  }
}

@media (max-width: 480px) {
  .project-rain-item {
    width: 80px;
    height: 80px;
  }
}

.project-image {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  border: 1px solid var(--black);
}
</style>
