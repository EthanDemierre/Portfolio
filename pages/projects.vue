<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]">
    <slider />
  </section>

 


  <main class="grid-container">
    <rain />
    <button ref="menuBtn" @click="toggleNav">
      <img src="public/img/menu.svg" alt="">
    </button>
    <section class="quote grid-item-quote">
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





.grid-item-quote {
  grid-column: 10 / span 3;
  grid-row: 10 / span 2;
  align-self: end;
  justify-self: start;
}



iframe {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  border: 0;
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

