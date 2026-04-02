<template>
  <!-- Section Contact -->
  <section id="contact" class="py-24 px-6 bg-white dark:bg-gray-950">
    <div class="max-w-6xl mx-auto">

      <!-- HEADER -->
      <div class="mb-14">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400 uppercase tracking-widest mb-3">
          // {{ t.contact.label }}
        </p>

        <h2 class="text-4xl md:text-5xl font-bold">
          {{ t.contact.title }}
        </h2>

        <p class="text-gray-500 dark:text-gray-400 mt-4">
          {{ t.contact.desc }}
        </p>
      </div>

      <div class="grid md:grid-cols-2 gap-12 items-start">

        <!-- LEFT: PROFILE + LINKS -->
        <div class="space-y-6">

          <!-- PHOTO -->
       

          <!-- LINKS -->
          <div class="space-y-4">

            <a v-for="link in links"
               :key="link.label"
               :href="link.href"
               target="_blank"
               class="flex items-center gap-4 p-4 rounded-xl
                      border border-gray-200 dark:border-gray-800
                      hover:border-emerald-500 hover:bg-emerald-50
                      dark:hover:bg-emerald-900/10
                      transition-all duration-300 group
                      hover:-translate-y-1 hover:shadow-lg">

              <!-- ICON -->
              <div class="w-10 h-10 flex items-center justify-center
                          transition-transform duration-300 group-hover:scale-110">

                <component :is="components[link.icon]" class="w-6 h-6" />

              </div>

              <!-- TEXT -->
              <div>
                <div class="font-mono text-xs text-gray-400">
                  {{ link.label }}
                </div>

                <div class="text-gray-700 dark:text-gray-300
                            group-hover:text-emerald-600 dark:group-hover:text-emerald-400">
                  {{ link.value }}
                </div>
              </div>

            </a>

          </div>
        </div>

        <!-- RIGHT: FORM -->
        <div class="space-y-4">

          <!-- NAME -->
          <div>
            <label class="font-mono text-xs text-emerald-600 uppercase block mb-2">
              {{ t.contact.name }}
            </label>

            <input v-model="form.name" type="text"
                   class="w-full px-4 py-3 rounded-lg text-sm
                          bg-gray-50 dark:bg-gray-900
                          border border-gray-200 dark:border-gray-700
                          focus:border-emerald-500 focus:outline-none"/>
          </div>

          <!-- EMAIL -->
          <div>
            <label class="font-mono text-xs text-emerald-600 uppercase block mb-2">
              {{ t.contact.email }}
            </label>

            <input v-model="form.email" type="email"
                   class="w-full px-4 py-3 rounded-lg text-sm
                          bg-gray-50 dark:bg-gray-900
                          border border-gray-200 dark:border-gray-700
                          focus:border-emerald-500 focus:outline-none"/>
          </div>

          <!-- MESSAGE -->
          <div>
            <label class="font-mono text-xs text-emerald-600 uppercase block mb-2">
              {{ t.contact.message }}
            </label>

            <textarea v-model="form.message" rows="5"
                      class="w-full px-4 py-3 rounded-lg text-sm
                             bg-gray-50 dark:bg-gray-900
                             border border-gray-200 dark:border-gray-700
                             focus:border-emerald-500 focus:outline-none resize-none">
            </textarea>
          </div>

          <!-- BUTTON -->
          <button @click="sendMessage"
                  class="w-full py-3 bg-emerald-600 hover:bg-emerald-700
                         text-white font-mono text-sm rounded-lg
                         transition-all hover:-translate-y-0.5
                         hover:shadow-lg">
            {{ t.contact.send }} →
          </button>

          <!-- SUCCESS -->
          <div v-if="sent"
               class="p-4 rounded-lg bg-emerald-50 dark:bg-emerald-900/20
                      border border-emerald-200 dark:border-emerald-800
                      text-emerald-600 text-center font-mono text-sm">
            ✓ {{ t.contact.success }}
          </div>

        </div>

      </div>
    </div>
  </section>
</template>

<script>
/* SVG ICONS */
const GmailIcon = {
  template: `
    <svg viewBox="0 0 24 24" fill="currentColor" class="text-red-500">
      <path d="M20 18V8l-8 5-8-5v10h16z"/>
      <path d="M20 6H4l8 5 8-5z"/>
    </svg>
  `
}

const GitHubIcon = {
  template: `
    <svg viewBox="0 0 24 24" fill="currentColor">
      <path d="M12 .5C5.7.5.5 5.7.5 12c0 5.1 3.3 9.4 7.9 10.9.6.1.8-.3.8-.6v-2.1c-3.2.7-3.9-1.4-3.9-1.4-.5-1.3-1.2-1.6-1.2-1.6-1-.7.1-.7.1-.7 1.1.1 1.7 1.2 1.7 1.2 1 .1 2.1-.7 2.1-.7.1-.8.4-1.4.7-1.7-2.5-.3-5.1-1.2-5.1-5.3 0-1.2.4-2.2 1.2-3-.1-.3-.5-1.4.1-2.9 0 0 1-.3 3.2 1.2a11 11 0 0 1 5.8 0C17.6 4.8 18.6 5.1 18.6 5.1c.6 1.5.2 2.6.1 2.9.8.8 1.2 1.8 1.2 3 0 4.1-2.6 5-5.1 5.3.4.4.8 1.1.8 2.2v3.3c0 .3.2.7.8.6A11.5 11.5 0 0 0 23.5 12C23.5 5.7 18.3.5 12 .5z"/>
    </svg>
  `
}

const LinkedInIcon = {
  template: `
    <svg viewBox="0 0 24 24" fill="currentColor" class="text-blue-600">
      <path d="M4.98 3.5C4.98 4.88 3.88 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 8h5v16H0V8zm7.5 0H12v2.2h.1c.6-1.2 2.1-2.4 4.3-2.4 4.6 0 5.5 3 5.5 6.9V24h-5v-7.5c0-1.8 0-4.1-2.5-4.1s-2.9 1.9-2.9 4V24h-5V8z"/>
    </svg>
  `
}

export default {
  name: 'ContactSection',

  components: {
    GmailIcon,
    GitHubIcon,
    LinkedInIcon
  },

  props: {
    t: Object
  },

  data() {
    return {
      profileImage: '/images/profile.jpg', // 👉 place ton image ici (public/images)

      form: {
        name: '',
        email: '',
        message: ''
      },

      sent: false,

     links: [
  {
    label: 'Email',
    value: 'moussaifsaad4@gmail.com',
    href: 'https://mail.google.com/...',
    icon: 'gmail.png'
  },
  {
    label: 'GitHub',
    value: 'github.com/moussaifsaad',
    href: 'https://github.com/saadmoussaif',
    icon: 'github.png'
  },
  {
    label: 'LinkedIn',
    value: 'linkedin.com/in/moussaifsaad',
    href: 'https://www.linkedin.com/...',
    icon: 'LinkedInIcon'  }
]
    }
  },

  computed: {
    components() {
      return {
        GmailIcon,
        GitHubIcon,
        LinkedInIcon
      }
    }
  },

  methods: {
    sendMessage() {
      if (this.form.name && this.form.email && this.form.message) {
        this.sent = true
        this.form = { name: '', email: '', message: '' }

        setTimeout(() => {
          this.sent = false
        }, 4000)
      }
    }
  }
}
</script>