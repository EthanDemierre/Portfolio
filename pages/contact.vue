<template>
  <page-nav />

  <main class="page-main">
    <section class="contact-content">
      <div class="contact-form-wrapper">
        <h2>Envoie moi un message.</h2>
        <form @submit.prevent="sendMessage" class="contact-form">
          <div class="form-row">
            <input
              v-model="form.firstName"
              type="text"
              placeholder="Ethan"
              class="form-input"
              required
            />
            <input
              v-model="form.lastName"
              type="text"
              placeholder="Demierre"
              class="form-input"
              required
            />
          </div>
          <div class="form-row">
            <input
              v-model="form.email"
              type="email"
              placeholder="ethandemierre@gmail.com"
              class="form-input"
              required
            />
            <input
              v-model="form.phone"
              type="tel"
              placeholder="079/657/54/43"
              class="form-input"
            />
          </div>
          <textarea
            v-model="form.message"
            placeholder="Je t'aime ethan"
            class="form-textarea"
            required
          ></textarea>
          <button type="submit" class="submit-btn">Envoyez</button>
        </form>

        <p v-if="successMessage" class="success-msg">{{ successMessage }}</p>
        <p v-if="errorMessage" class="error-msg">{{ errorMessage }}</p>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue'
import emailjs from 'emailjs-com'

const showNav = ref(false)

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
      errorMessage.value = 'Erreur lors de l\'envoi. Réessaie plus tard.'
    })
}
</script>

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

.contact-content {
  grid-column: 3 / span 8;
  grid-row: 3 / span 8;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  pointer-events: auto;
}

@media (max-width: 1440px) {
  .contact-content {
    grid-column: 3 / span 8;
    grid-row: 3 / span 8;
  }
}

@media (max-width: 1024px) {
  .contact-content {
    grid-column: 2 / span 10;
    grid-row: 3 / span 8;
  }
}

@media (max-width: 768px) {
  .contact-content {
    grid-column: 1 / span 12;
    grid-row: 2 / span 10;
  }
}

@media (max-width: 480px) {
  .contact-content {
    grid-column: 1 / -1;
    grid-row: 2 / span 10;
    padding: 1rem;
  }
}

.contact-form-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.form-row {
  display: flex;
  gap: 1rem;
}

@media (max-width: 768px) {
  .form-row {
    gap: 0.75rem;
  }
}

@media (max-width: 480px) {
  .form-row {
    flex-direction: column;
    gap: 0.75rem;
  }
}

.form-input,
.form-textarea {
  padding: 1rem;
  font-family: inherit;
  border: 1px solid var(--black);
  font-size: 1rem;
}

.form-input {
  flex: 1;
}

.form-textarea {
  width: 100%;
  min-height: 150px;
  resize: vertical;
}

@media (max-width: 768px) {
  .form-input,
  .form-textarea {
    padding: 0.75rem;
    font-size: 0.9rem;
  }

  .form-textarea {
    min-height: 120px;
  }
}

@media (max-width: 480px) {
  .form-input,
  .form-textarea {
    padding: 0.75rem;
    font-size: 0.85rem;
  }

  .form-textarea {
    min-height: 100px;
  }
}

.submit-btn {
  padding: 1rem 2rem;
  background-color: var(--blue);
  color: white;
  border: none;
  cursor: pointer;
  font-weight: bold;
  font-style: italic;
  width: fit-content;
  align-self: center;
}

@media (max-width: 480px) {
  .submit-btn {
    width: 100%;
    padding: 0.875rem 1.5rem;
  }
}

.success-msg {
  color: green;
  text-align: center;
}

.error-msg {
  color: red;
  text-align: center;
}

h2 {
  width: 100%;
  text-align: center;
}
</style>
