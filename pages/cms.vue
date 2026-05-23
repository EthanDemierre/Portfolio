<template>
  <div class="cms-page">
    <header class="cms-header">
      <h1 class="cms-title">Gestion des Projets</h1>
      <button @click="goHome" class="back-btn">← Retour</button>
    </header>

    <main class="cms-main">
      <button @click="addProject" class="btn-add-project">+ Ajouter un projet</button>

      <div v-if="projects.length === 0" class="empty-state">
        <p>Aucun projet. Cliquez sur "Ajouter un projet" pour commencer.</p>
      </div>

      <div class="projects-list">
        <div v-for="(project, index) in projects" :key="project.id" class="project-card">
          <div class="project-header">
            <h3 class="project-title">{{ project.title }}</h3>
            <button @click="removeProject(index)" class="btn-delete" title="Supprimer">🗑️</button>
          </div>

          <div class="form-group">
            <label class="form-label">Titre</label>
            <input v-model="project.title" type="text" class="form-input" placeholder="Titre du projet">
          </div>

          <div class="form-group">
            <label class="form-label">Date</label>
            <input v-model="project.date" type="text" class="form-input" placeholder="2024">
          </div>

          <div class="form-group">
            <label class="form-label">Description</label>
            <textarea v-model="project.description" class="form-textarea" placeholder="Description du projet" rows="3"></textarea>
          </div>

          <div class="form-group">
            <label class="form-label">Catégorie (Design, Animation, etc.)</label>
            <input v-model="project.medium" type="text" class="form-input" placeholder="Ex: Design / Web">
          </div>

          <div class="form-group">
            <label class="form-label">URL de l'image</label>
            <input v-model="project.image" type="text" class="form-input" placeholder="/img/projet/projet1.png">
            <div v-if="project.image" class="image-preview">
              <img :src="project.image" :alt="project.title" class="preview-img">
            </div>
          </div>
        </div>
      </div>

      <div class="cms-actions">
        <button @click="saveProjects" class="btn-save">✓ Sauvegarder les changements</button>
        <button @click="resetProjects" class="btn-cancel">✕ Annuler</button>
      </div>

      <div v-if="message" :class="['message', message.type]">
        {{ message.text }}
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      projects: [],
      originalProjects: [],
      message: null
    };
  },
  async mounted() {
    await this.loadProjects();
  },
  methods: {
    async loadProjects() {
      try {
        const response = await fetch('/api/projects');
        this.projects = await response.json();
        this.originalProjects = JSON.parse(JSON.stringify(this.projects));
      } catch (error) {
        console.error('Erreur lors du chargement des projets:', error);
        this.showMessage('Erreur lors du chargement', 'error');
      }
    },
    addProject() {
      const newId = Math.max(...this.projects.map(p => p.id), 0) + 1;
      this.projects.push({
        id: newId,
        title: 'Nouveau Projet',
        image: '',
        date: new Date().getFullYear().toString(),
        description: '',
        medium: ''
      });
    },
    removeProject(index) {
      if (confirm('Êtes-vous sûr de vouloir supprimer ce projet ?')) {
        this.projects.splice(index, 1);
      }
    },
    async saveProjects() {
      try {
        const response = await fetch('/api/projects', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(this.projects)
        });
        const result = await response.json();
        if (result.success) {
          this.originalProjects = JSON.parse(JSON.stringify(this.projects));
          this.showMessage('Projets sauvegardés avec succès !', 'success');
        } else {
          this.showMessage('Erreur lors de la sauvegarde', 'error');
        }
      } catch (error) {
        console.error('Erreur:', error);
        this.showMessage('Erreur lors de la sauvegarde', 'error');
      }
    },
    resetProjects() {
      if (confirm('Annuler tous les changements ?')) {
        this.projects = JSON.parse(JSON.stringify(this.originalProjects));
      }
    },
    showMessage(text, type) {
      this.message = { text, type };
      setTimeout(() => { this.message = null; }, 3000);
    },
    goHome() {
      this.$router.push('/');
    }
  }
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.cms-page {
  min-height: 100vh;
  background-color: white;
  padding: 2rem;
  font-family: 'DM Mono', monospace;
}

.cms-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3rem;
  padding-bottom: 2rem;
  border-bottom: 2px solid var(--blue);
}

.cms-title {
  font-size: 2rem;
  color: var(--black);
  margin: 0;
  font-weight: 600;
}

.back-btn {
  background: none;
  border: 2px solid var(--blue);
  color: var(--blue);
  padding: 0.75rem 1.5rem;
  border-radius: 4px;
  cursor: pointer;
  font-family: 'DM Mono', monospace;
  font-size: 0.95rem;
  transition: all 0.3s ease;
}

.back-btn:hover {
  background-color: var(--blue);
  color: white;
}

.cms-main {
  max-width: 900px;
  margin: 0 auto;
}

.btn-add-project {
  display: block;
  width: 100%;
  padding: 1.5rem;
  margin-bottom: 2rem;
  background-color: var(--blue);
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1.1rem;
  font-family: 'DM Mono', monospace;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-add-project:hover {
  background-color: #0066cc;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.empty-state {
  text-align: center;
  padding: 3rem;
  color: #999;
  font-size: 1.1rem;
}

.projects-list {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  margin-bottom: 2rem;
}

.project-card {
  border: 2px solid #ddd;
  border-radius: 8px;
  padding: 2rem;
  background-color: #fafafa;
  transition: all 0.3s ease;
}

.project-card:hover {
  border-color: var(--blue);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

.project-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #ddd;
}

.project-title {
  margin: 0;
  color: var(--black);
  font-size: 1.3rem;
  flex: 1;
}

.btn-delete {
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  transition: transform 0.2s ease;
  padding: 0.5rem;
}

.btn-delete:hover {
  transform: scale(1.2);
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 600;
  color: var(--black);
  font-size: 0.95rem;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-family: 'DM Mono', monospace;
  font-size: 0.95rem;
  transition: all 0.3s ease;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: var(--blue);
  box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 80px;
}

.image-preview {
  margin-top: 1rem;
  padding: 1rem;
  background-color: white;
  border-radius: 4px;
  text-align: center;
}

.preview-img {
  max-width: 100%;
  max-height: 200px;
  object-fit: contain;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.cms-actions {
  display: flex;
  gap: 1rem;
  margin-top: 3rem;
  padding-top: 2rem;
  border-top: 2px solid var(--blue);
}

.btn-save,
.btn-cancel {
  flex: 1;
  padding: 1.25rem;
  border: none;
  border-radius: 4px;
  font-family: 'DM Mono', monospace;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-save {
  background-color: var(--blue);
  color: white;
}

.btn-save:hover {
  background-color: #0066cc;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.btn-cancel {
  background-color: #f0f0f0;
  color: #666;
  border: 1px solid #ddd;
}

.btn-cancel:hover {
  background-color: #e0e0e0;
}

.message {
  margin-top: 1.5rem;
  padding: 1rem;
  border-radius: 4px;
  text-align: center;
  font-weight: 600;
  animation: slideIn 0.3s ease;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.message.success {
  background-color: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.message.error {
  background-color: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

@media (max-width: 768px) {
  .cms-page {
    padding: 1rem;
  }

  .cms-header {
    flex-direction: column;
    gap: 1rem;
    align-items: flex-start;
  }

  .cms-title {
    font-size: 1.5rem;
  }

  .back-btn {
    width: 100%;
  }

  .project-card {
    padding: 1rem;
  }

  .cms-actions {
    flex-direction: column;
  }
}
</style>
