<template>
  <nav class="nav-menu">
    <ul class="nav-list">
      <li><a href="/">Home</a></li>
      <li><a href="/about">À propos</a></li>
      <li><a href="/projects">Projets</a></li>
      <li><a href="/contact">Contact</a></li>
      <li><a href="/cms">CMS</a></li>
    </ul>
  </nav>
</template>

<style scoped>
.nav-menu {
  width: 100%;
  height: 100%;
}

.nav-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  list-style: none;
  height: 100%;
  padding: 0;
  margin: 0;
}

.nav-list li {
  text-align: center;
  padding: 1.5rem;
}

.nav-list a {
  text-decoration: none;
  color: white;
}

.nav-list a:hover {
  opacity: 0.8;
}
</style>
