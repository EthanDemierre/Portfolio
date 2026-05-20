<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]"
  >
    <slider />
  </section>

  <iframe
    style="width:100vw;height:100vh;border:0px;"
    allow="autoplay;"
    src="https://cables.gl/view/tduqhJ"
  ></iframe>

  <main class="grid-container">
    <button ref="menuBtn" @click="toggleNav" class="hamburger" :class="{ 'hamburger--active': showNav }">
      <span class="hamburger-line"></span>
      <span class="hamburger-line"></span>
      <span class="hamburger-line"></span>
    </button>

    <section class="content grid-item-main">
      <div class="moi">
        <div class="name-with-flower">
          <img src="public/img/fleur.svg" alt="fleur" class="flower-icon">
          <h1>Ethan Demierre</h1>
        </div>
        <div class="imd">
          <h4>Interactive Media Designer.</h4>
        </div>
      </div>
    </section>

    <section class="quote grid-item-quote">
      <p><b>factotum</b> \fak.tɔ.tɔm\</p>
      <p>
        Emprunté au latin de la Renaissance <b>factotum</b> («fais tout»),
        du latin facere («faire») et <b>totum</b> («tout»).
      </p>
    </section>
  </main>
</template>

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

button.hamburger {
  background: none;
  border: none;
  cursor: pointer;
  position: fixed;
  top: 2.2rem;
  left: 2.2rem;
  z-index: 20;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
  width: 1.8rem;
  height: auto;
}

.hamburger-line {
  width: 1.8rem;
  height: 0.15rem;
  background-color: var(--black);
  transition: all 0.3s ease-in-out;
  transform-origin: center;
}

.hamburger--active .hamburger-line:nth-child(1) {
  transform: rotate(45deg) translateY(0.55rem);
}

.hamburger--active .hamburger-line:nth-child(2) {
  opacity: 0;
}

.hamburger--active .hamburger-line:nth-child(3) {
  transform: rotate(-45deg) translateY(-0.55rem);
}

@media (max-width: 1440px) {
  button.hamburger {
    top: 2rem;
    left: 2rem;
  }
}

@media (max-width: 1024px) {
  button.hamburger {
    top: 1.75rem;
    left: 1.75rem;
    width: 1.6rem;
    gap: 0.35rem;
  }

  .hamburger-line {
    width: 1.6rem;
    height: 0.13rem;
  }

  .hamburger--active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(0.48rem);
  }

  .hamburger--active .hamburger-line:nth-child(3) {
    transform: rotate(-45deg) translateY(-0.48rem);
  }
}

@media (max-width: 768px) {
  button.hamburger {
    top: 1.25rem;
    left: 1.25rem;
    width: 1.5rem;
    gap: 0.35rem;
  }

  .hamburger-line {
    width: 1.5rem;
    height: 0.13rem;
  }

  .hamburger--active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(0.45rem);
  }

  .hamburger--active .hamburger-line:nth-child(3) {
    transform: rotate(-45deg) translateY(-0.45rem);
  }
}

@media (max-width: 480px) {
  button.hamburger {
    top: 0.75rem;
    left: 0.75rem;
    width: 1.2rem;
    gap: 0.3rem;
  }

  .hamburger-line {
    width: 1.2rem;
    height: 0.12rem;
  }

  .hamburger--active .hamburger-line:nth-child(1) {
    transform: rotate(45deg) translateY(0.36rem);
  }

  .hamburger--active .hamburger-line:nth-child(3) {
    transform: rotate(-45deg) translateY(-0.36rem);
  }
}

.grid-container {
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  padding: 2rem;
  border: 1rem solid var(--blue);
  pointer-events: none;
}

.grid-container button,
.grid-container section {
  pointer-events: auto;
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

.grid-item-main {
  grid-column: 4 / span 6;
  grid-row: 6 / span 3;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

@media (max-width: 1440px) {
  .grid-item-main {
    grid-column: 4 / span 5;
    grid-row: 5 / span 3;
  }
}

@media (max-width: 1024px) {
  .grid-item-main {
    grid-column: 3 / span 7;
    grid-row: 5 / span 3;
  }
}

@media (max-width: 768px) {
  .grid-item-main {
    grid-column: 2 / span 10;
    grid-row: 4 / span 4;
  }
}

@media (max-width: 480px) {
  .grid-item-main {
    grid-column: 1 / -1;
    grid-row: 3 / span 4;
    padding: 1rem;
  }
}

.moi {
  display: grid;
  grid-template-columns: 1fr;
  gap: 0rem;
  align-items: center;
  text-align: center;
}

.name-with-flower {
  position: relative;
  display: inline-block;
  width: 100%;
}

.flower-icon {
  position: absolute;
  width: 8rem;
  height: 8rem;
  top: -1.5rem;
  left: 2.5rem;
  z-index: 2;
}

@media (max-width: 1440px) {
  .flower-icon {
    width: 7.5rem;
    height: 7.5rem;
    left: 2.25rem;
  }
}

@media (max-width: 1024px) {
  .flower-icon {
    width: 6.5rem;
    height: 6.5rem;
    left: 2rem;
  }
}

@media (max-width: 768px) {
  .flower-icon {
    width: 5rem;
    height: 5rem;
    left: 1.5rem;
    top: -1rem;
  }
}

@media (max-width: 480px) {
  .flower-icon {
    width: 3.5rem;
    height: 3.5rem;
    left: 0.75rem;
    top: -0.5rem;
  }
}

h1 {
  max-width: 100%;
}

.imd {
  display: inline-block;
  padding: 1.3rem;
  border: 1px solid;
  width: 33%;
  background-color: white;
}

@media (max-width: 1024px) {
  .imd {
    width: 35%;
    padding: 1.1rem;
  }
}

@media (max-width: 768px) {
  .imd {
    width: 50%;
    padding: 1rem;
  }
}

@media (max-width: 480px) {
  .imd {
    width: 100%;
    padding: 0.75rem;
  }
}

.grid-item-quote {
  grid-column: 10 / span 3;
  grid-row: 10 / span 2;
  align-self: end;
  justify-self: start;
}

@media (max-width: 1440px) {
  .grid-item-quote {
    grid-column: 9 / span 4;
    grid-row: 10 / span 2;
  }
}

@media (max-width: 1024px) {
  .grid-item-quote {
    grid-column: 8 / span 5;
    grid-row: 9 / span 2;
  }
}

@media (max-width: 768px) {
  .grid-item-quote {
    grid-column: 1 / span 12;
    grid-row: 8 / span 2;
    align-self: auto;
    justify-self: auto;
  }
}

@media (max-width: 480px) {
  .grid-item-quote {
    grid-column: 1 / -1;
    grid-row: 7 / span 3;
  }
}

.quote p {
  width: 75%;
  margin-bottom: 0.5rem;
  font-size: 0.8rem;
  text-align: left;
}

@media (max-width: 1024px) {
  .quote p {
    width: 85%;
    font-size: 0.8rem;
  }
}

@media (max-width: 768px) {
  .quote p {
    width: 100%;
    font-size: 0.75rem;
  }
}

@media (max-width: 480px) {
  .quote p {
    width: 100%;
    font-size: 0.7rem;
    margin-bottom: 0.25rem;
  }
}

.grid-item-nav {
  grid-column: 1 / -1;
  grid-row: 1;
  display: flex;
  justify-content: start;
  padding: 1rem;
}

iframe {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 2;
  pointer-events: auto;
}

main {
  position: relative;
  z-index: 20;
}


</style>

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
