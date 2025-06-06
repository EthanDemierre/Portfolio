<template>
  <section
    ref="nav"
    :class="['navigation', { 'navigation--active': showNav }]"
  >
    <slider />
  </section>

  <main class="grid-container">
    <button ref="menuBtn" @click="toggleNav">
      <img src="/img/menu.svg" alt="menu" />
    </button>

    <section class="content grid-item-main">
      <div class="contact-form">
        <b>Envoie moi un message.</b>
        <form @submit.prevent="sendMessage">
          <div class="form-row">
            <input v-model="form.firstName" type="text" placeholder="Ethan" required />
            <input v-model="form.lastName" type="text" placeholder="Demierre" required />
          </div>
          <div class="form-row">
            <input v-model="form.email" type="email" placeholder="ethandemierre@gmail.com" required />
            <input v-model="form.phone" type="tel" placeholder="079/657/54/43" />
          </div>
          <textarea v-model="form.message" placeholder="Je t’aime ethan" required></textarea>
          <button type="submit">Envoyez</button>
        </form>

        <p v-if="successMessage" class="success">{{ successMessage }}</p>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
      </div>
    </section>

    <section class="quote grid-item-quote">
   
    </section>
  </main>
</template>

<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue'
import emailjs from 'emailjs-com'

const showNav = ref(false)
const nav = ref(null)
const menuBtn = ref(null)

const toggleNav = () => {
  showNav.value = !showNav.value
}

const handleClickOutside = (event) => {
  if (
    showNav.value &&
    nav.value &&
    !nav.value.contains(event.target) &&
    menuBtn.value &&
    !menuBtn.value.contains(event.target)
  ) {
    showNav.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleClickOutside)
})

// EmailJS config
const form = reactive({
  firstName: '',
  lastName: '',
  email: '',
  phone: '',
  message: ''
})

const successMessage = ref('')
const errorMessage = ref('')

const SERVICE_ID = 'service_xxx'
const TEMPLATE_ID = 'template_xxx'
const PUBLIC_KEY = 'public_xxx'

const sendMessage = () => {
  emailjs.send(SERVICE_ID, TEMPLATE_ID, form, PUBLIC_KEY)
    .then(() => {
      successMessage.value = 'Message envoyé avec succès !'
      errorMessage.value = ''
      form.firstName = ''
      form.lastName = ''
      form.email = ''
      form.phone = ''
      form.message = ''
    })
    .catch(() => {
      successMessage.value = ''
      errorMessage.value = 'Erreur lors de l’envoi. Réessaie plus tard.'
    })
}
</script>

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

.grid-container {
  box-sizing: border-box;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  padding: 2rem;
  border: 1rem solid var(--blue);
}

button {
  background: none;
  border: none;
  cursor: pointer;
}

.grid-item-main {
  grid-column: 4 / span 6;
  grid-row: 4 / span 6;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  font-family: monospace;
}

.contact-form h1 {
  font-size: 2rem;
  font-weight: bold;
}

.form-row {
  display: flex;
  gap: 1rem;
}

input,
textarea {
  width: 100%;
  padding: 1rem;
  font-family: monospace;
  border: 1px solid black;
  font-size: 1rem;
  margin: 0.5rem;
}

textarea {
  min-height: 150px;
}

button[type="submit"] {
  font-weight: bold;
  font-style: italic;
  background-color: var(--blue);
  color: white;
  padding: 1rem 2rem;
  border: none;
  width: fit-content;
}

.success {
  color: green;
}

.error {
  color: red;
}

.grid-item-quote {
  grid-column: 10 / span 3;
  grid-row: 10 / span 2;
  align-self: end;
  justify-self: start;
  font-family: monospace;
}

.quote p {
  width: 75%;
  margin-bottom: 0.5rem;
  font-size: 0.8rem;
  text-align: left;
}

b {
  color: #000;
font-family: "Coral Pixels";
font-size: 2rem;
font-style: normal;
font-weight: 400;
line-height: 1rem; /* 50% */
letter-spacing: 0.1rem;
}
</style>
