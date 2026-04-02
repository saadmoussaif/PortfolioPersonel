<template>
  <!-- Section Contact -->
  <section id="contact" class="py-24 px-6 bg-white dark:bg-gray-950">
    <div class="max-w-5xl mx-auto">

      <!-- Label + Titre -->
      <div class="mb-14">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                  uppercase tracking-widest mb-3">
          // {{ t.contact.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold">{{ t.contact.title }}</h2>
        <p class="text-gray-500 dark:text-gray-400 mt-4">{{ t.contact.desc }}</p>
      </div>

      <div class="grid md:grid-cols-2 gap-12">

        <!-- Liens de contact -->
        <div class="space-y-4">
          <a v-for="link in links" :key="link.label"
             :href="link.href"
             class="flex items-center gap-4 p-4 rounded-xl
                    border border-gray-200 dark:border-gray-800
                    hover:border-emerald-500 hover:bg-emerald-50
                    dark:hover:bg-emerald-900/10
                    transition-all group">
            <span class="text-2xl">{{ link.icon }}</span>
            <div>
              <div class="font-mono text-xs text-gray-400">{{ link.label }}</div>
              <div class="text-gray-700 dark:text-gray-300 group-hover:text-emerald-600
                          dark:group-hover:text-emerald-400 transition-colors">
                {{ link.value }}
              </div>
            </div>
          </a>
        </div>

        <!-- Formulaire de contact -->
        <div class="space-y-4">

          <!-- Nom -->
          <div>
            <label class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                          uppercase tracking-wider block mb-2">
              {{ t.contact.name }}
            </label>
            <input v-model="form.name" type="text"
                   :placeholder="t.contact.name"
                   class="w-full px-4 py-3 rounded-lg text-sm
                          bg-gray-50 dark:bg-gray-900
                          border border-gray-200 dark:border-gray-700
                          focus:border-emerald-500 focus:outline-none
                          text-gray-900 dark:text-white
                          transition-colors" />
          </div>

          <!-- Email -->
          <div>
            <label class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                          uppercase tracking-wider block mb-2">
              {{ t.contact.email }}
            </label>
            <input v-model="form.email" type="email"
                   :placeholder="t.contact.email"
                   class="w-full px-4 py-3 rounded-lg text-sm
                          bg-gray-50 dark:bg-gray-900
                          border border-gray-200 dark:border-gray-700
                          focus:border-emerald-500 focus:outline-none
                          text-gray-900 dark:text-white
                          transition-colors" />
          </div>

          <!-- Message -->
          <div>
            <label class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                          uppercase tracking-wider block mb-2">
              {{ t.contact.message }}
            </label>
            <textarea v-model="form.message" rows="4"
                      :placeholder="t.contact.message"
                      class="w-full px-4 py-3 rounded-lg text-sm
                             bg-gray-50 dark:bg-gray-900
                             border border-gray-200 dark:border-gray-700
                             focus:border-emerald-500 focus:outline-none
                             text-gray-900 dark:text-white
                             transition-colors resize-none">
            </textarea>
          </div>

          <!-- Bouton envoyer -->
          <button @click="sendMessage"
                  class="w-full py-3 bg-emerald-600 hover:bg-emerald-700
                         text-white font-mono text-sm rounded-lg
                         transition-all hover:-translate-y-0.5
                         hover:shadow-lg hover:shadow-emerald-500/25">
            {{ t.contact.send }} →
          </button>

          <!-- Message de succès -->
          <div v-if="sent"
               class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20
                      border border-emerald-200 dark:border-emerald-800
                      text-emerald-600 dark:text-emerald-400
                      font-mono text-sm text-center">
            ✓ {{ t.contact.success }}
          </div>

        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection',

  props: {
    t: Object,
  },

  data() {
    return {
      // Données du formulaire
      form: {
        name: '',
        email: '',
        message: '',
      },

      // Afficher le message de succès
      sent: false,

      // Liens de contact
      links: [
        { icon: '✉', label: 'Email', value: 'alex@email.com', href: 'mailto:alex@email.com' },
        { icon: '💻', label: 'GitHub', value: 'github.com/alexmartin', href: '#' },
        { icon: '💼', label: 'LinkedIn', value: 'linkedin.com/in/alexmartin', href: '#' },
      ],
    }
  },

  methods: {
    sendMessage() {
      // Vérifier que tous les champs sont remplis
      if (this.form.name && this.form.email && this.form.message) {
        this.sent = true
        // Réinitialiser le formulaire
        this.form = { name: '', email: '', message: '' }
        // Cacher le message après 4 secondes
        setTimeout(() => { this.sent = false }, 4000)
      }
    },
  },
}
</script>