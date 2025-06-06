<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]">
    <slider />
  </section>

  <main class="grid-container">
    <!-- Bouton menu -->
    <button ref="menuBtn" @click="toggleNav">
      <img src="public/img/menu.svg" alt="menu">
    </button>

    <!-- Carrés centrés -->
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

    <!-- Texte -->
    <section class="content">
      <div class="aboutme">
        <p>
          J'ai 21 ans et je viens de terminer mes études à l’ERACOM. Passionné par la création sous toutes ses formes,
          j'aime imaginer, construire, transformer des idées en expériences visuelles et interactives. Le mixmedia est pour moi un super moyen d’expression.
        </p>
        <p>
          Si je devais m’identifier à des couleurs je serais le rouge (<span style="color: red;">FF0000</span>) et le bleu (<span style="color: #2600FF;">2600FF</span>)
          car...
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
  z-index: 5;
  width: 25%;
  height: 100vh;
  background-color: var(--blue);
  box-shadow: 0 0px 10px rgb(0, 0, 0);
  transform: translateX(-100%);
  transition: transform 0.4s ease-in-out;
}

.navigation--active {
  transform: translateX(0);
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

button {
  background: none;
  border: none;
  position: absolute;
  top: 1rem;
  left: 1rem;
  z-index: 10;
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
  gap: 600px; /* Espace large entre les deux carrés */
}

.aboutme {
  max-width: 800px;
  margin: 0 auto;
  text-align: left;
  font-family: monospace;
  font-size: 14px;
  padding-bottom: 2rem;
  line-height: 1.6;
}
</style>
