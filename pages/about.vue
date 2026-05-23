<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]">
    <slider />
  </section>

  <main class="grid-container">
    <button ref="menuBtn" @click="toggleNav">
      <img src="public/img/menu.svg" alt="menu">
    </button>

    <div class="carre-wrapper">
      <div class="carre">
        <svg xmlns="http://www.w3.org/2000/svg" width="68" height="68" viewBox="0 0 68 68" fill="none">
          <rect width="68" height="68" fill="#2600FF"/>
        </svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="68" height="68" viewBox="0 0 68 68" fill="none">
          <rect width="68" height="68" fill="#FF0000"/>
        </svg>
      </div>
    </div>

    <section class="content">
      <div class="aboutme">
        <p>
          J'ai 22 ans titulaire d'un CFC <b> D'interactive média designer.</b>  Passionné par la création sous toutes ses formes,
          j'aime imaginer, construire, transformer des idées en expériences visuelles et interactives. Le mixmedia est pour moi un super moyen d'expression.
        </p>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  data() {
    return {
      showNav: false
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
    }
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside);
  },
  beforeUnmount() {
    document.removeEventListener('click', this.handleClickOutside);
  }
};
</script>

<style scoped>
:root {
  --blue: #2600FF;
}

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
  padding: 2rem;
  border: 1rem solid var(--blue);
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background: white;
}

.carre-wrapper {
  flex-grow: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carre {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 600px;
}

@media (max-width: 1440px) {
  .carre {
    gap: 500px;
  }
}

@media (max-width: 1024px) {
  .carre {
    gap: 300px;
  }
}

@media (max-width: 768px) {
  .carre {
    gap: 150px;
  }
}

@media (max-width: 480px) {
  .carre {
    gap: 80px;
  }
}

.carre svg {
  width: 68px;
  height: 68px;
}

@media (max-width: 1024px) {
  .carre svg {
    width: 55px;
    height: 55px;
  }
}

@media (max-width: 768px) {
  .carre svg {
    width: 45px;
    height: 45px;
  }
}

@media (max-width: 480px) {
  .carre svg {
    width: 35px;
    height: 35px;
  }
}

.content {
  margin-top: auto;
  padding-bottom: 2rem;
}

.aboutme {
  max-width: 800px;
  margin: 0 auto;
  text-align: left;
  font-family: monospace;
  font-size: 14px;
  line-height: 1.6;
}

.aboutme p {
  margin-bottom: 1.5rem;
}

@media (max-width: 768px) {
  .aboutme {
    max-width: 100%;
    font-size: 13px;
  }
}

@media (max-width: 480px) {
  .aboutme {
    max-width: 100%;
    font-size: 12px;
    margin-bottom: 1rem;
  }

  .aboutme p {
    margin-bottom: 1rem;
  }
}

.red-text {
  color: red;
}

.blue-text {
  color: #2600FF;
}
</style>
