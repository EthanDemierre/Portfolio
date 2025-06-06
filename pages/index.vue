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
    <button ref="menuBtn" @click="toggleNav">
      <img src="public/img/menu.svg" alt="">
    </button>

    <section class="content grid-item-main">
      <div class="moi">
        <h1>Ethan Demierre</h1>
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

button {
  background: none;
  border: none;
}

.grid-container {
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  padding: 2rem;
  border: 1rem solid var(--blue);
}

.grid-item-main {
  grid-column: 4 / span 6;
  grid-row: 6 / span 3;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.moi {
  display: grid;
  grid-template-columns: 1fr;
  gap: 0rem;
  align-items: center;
  text-align: center;
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

.grid-item-quote {
  grid-column: 10 / span 3;
  grid-row: 10 / span 2;
  align-self: end;
  justify-self: start;
}

.quote p {
  width: 75%;
  margin-bottom: 0.5rem;
  font-size: 0.8rem;
  text-align: left;
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
  width: 100vw;
  height: 100vh;
  transform: translateX(-3);
  
}

main {
  position: relative;
  pointer-events: auto;
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
