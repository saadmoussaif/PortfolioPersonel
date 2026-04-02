<template>
  <!-- Navbar fixe en haut avec fond bleu foncé -->
  <nav :class="[
    'fixed top-0 left-0 right-0 z-50 transition-all duration-500',
    scrolled
      ? 'bg-blue-950/95 backdrop-blur-lg shadow-lg shadow-blue-950/50 border-b border-blue-800/50'
      : 'bg-blue-900/90 backdrop-blur-md border-b border-blue-800/30'
  ]">
    <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">

      <!-- ─── LOGO + PHOTO PERSONNELLE ─────────────────── -->
      <div class="flex items-center gap-3">

  <!-- LOGO SM DESIGN -->
  <div class="relative w-10 h-10 flex items-center justify-center">
    
    <!-- Glow -->
    <div class="absolute inset-0 rounded-full bg-emerald-400 blur-md opacity-40"></div>

    <!-- Cercle principal -->
    <div class="relative w-10 h-10 rounded-full flex items-center justify-center
                bg-gradient-to-br from-emerald-400 to-blue-500
                text-white font-bold text-sm
                shadow-lg
                hover:scale-110 hover:rotate-6
                transition-all duration-300">
      SM
    </div>

  </div>

  <!-- TEXTE SAADdev -->
  <span class="font-mono font-bold text-lg cursor-pointer"
        @click="scrollToTop">
    <span class="text-emerald-400">SAAD</span>
    <span class="text-blue-400">dev</span>
  </span>

</div>
      <!-- ─── LIENS NAVIGATION DESKTOP ─────────────────── -->
      <div class="hidden md:flex items-center gap-2">
        <a v-for="item in navItems" :key="item"
           @click="scrollTo(item)"
           @mouseenter="hoveredItem = item"
           @mouseleave="hoveredItem = null"
           :class="[
             'relative px-4 py-2 text-sm font-mono cursor-pointer',
             'rounded-lg transition-all duration-300',
             activeSection === item
               ? 'text-emerald-400 bg-blue-800/60'
               : 'text-gray-300 hover:text-white'
           ]">

          <!-- Fond animé au hover -->
          <span :class="[
            'absolute inset-0 rounded-lg transition-all duration-300',
            hoveredItem === item && activeSection !== item
              ? 'bg-blue-800/40 scale-100 opacity-100'
              : 'bg-blue-800/0 scale-95 opacity-0'
          ]"></span>

          <!-- Texte du lien -->
          <span class="relative z-10 flex items-center gap-1.5">
            <!-- Icône qui apparaît au hover -->
            <span :class="[
              'text-emerald-400 transition-all duration-300 text-xs',
              hoveredItem === item || activeSection === item
                ? 'opacity-100 translate-x-0'
                : 'opacity-0 -translate-x-2'
            ]">▹</span>
            {{ item }}
          </span>

          <!-- Indicateur actif en bas -->
          <span :class="[
            'absolute bottom-0 left-1/2 -translate-x-1/2',
            'h-0.5 bg-emerald-400 rounded-full',
            'transition-all duration-400',
            activeSection === item ? 'w-6 opacity-100' : 'w-0 opacity-0'
          ]"></span>

        </a>
      </div>

      <!-- ─── BOUTONS DROITE ─────────────────────────────── -->
      <div class="flex items-center gap-3">

        <!-- Bouton langue FR/EN -->
        <button @click="$emit('toggleLang')"
                class="relative font-mono text-xs px-3 py-1.5 rounded-full
                       border border-blue-600 text-gray-300
                       hover:border-emerald-400 hover:text-emerald-400
                       hover:bg-emerald-400/10
                       transition-all duration-300 overflow-hidden group">
          <!-- Animation de fond au hover -->
          <span class="absolute inset-0 bg-emerald-400/5 
                       scale-0 group-hover:scale-100 
                       rounded-full transition-transform duration-300"></span>
          <span class="relative">{{ lang === 'fr' ? 'EN' : 'FR' }}</span>
        </button>

        <!-- Bouton mode nuit/jour -->
        <button @click="$emit('toggleDark')"
                class="w-9 h-9 rounded-full flex items-center justify-center
                       border border-blue-600 text-gray-200
                       hover:border-emerald-400 hover:bg-emerald-400/10
                       transition-all duration-300 hover:rotate-12
                       hover:scale-110">
          <span class="transition-all duration-300 text-base">
            {{ isDark ? '☀️' : '🌙' }}
          </span>
        </button>

        <!-- Menu hamburger mobile -->
        <button @click="mobileOpen = !mobileOpen"
                class="md:hidden w-9 h-9 rounded-full flex flex-col items-center 
                       justify-center gap-1.5 border border-blue-600
                       hover:border-emerald-400 transition-all duration-300">
          <span :class="[
            'w-4 h-0.5 bg-gray-300 rounded transition-all duration-300',
            mobileOpen ? 'rotate-45 translate-y-2' : ''
          ]"></span>
          <span :class="[
            'w-4 h-0.5 bg-gray-300 rounded transition-all duration-300',
            mobileOpen ? 'opacity-0' : ''
          ]"></span>
          <span :class="[
            'w-4 h-0.5 bg-gray-300 rounded transition-all duration-300',
            mobileOpen ? '-rotate-45 -translate-y-2' : ''
          ]"></span>
        </button>

      </div>
    </div>

    <!-- ─── MENU MOBILE ───────────────────────────────────── -->
    <div :class="[
      'md:hidden overflow-hidden transition-all duration-400',
      mobileOpen ? 'max-h-64 opacity-100' : 'max-h-0 opacity-0'
    ]">
      <div class="px-6 py-4 border-t border-blue-800/50 flex flex-col gap-2">
        <a v-for="item in navItems" :key="item"
           @click="scrollTo(item); mobileOpen = false"
           :class="[
             'px-4 py-3 rounded-lg font-mono text-sm cursor-pointer',
             'transition-all duration-200',
             activeSection === item
               ? 'bg-blue-800 text-emerald-400'
               : 'text-gray-300 hover:bg-blue-800/50 hover:text-white'
           ]">
          <span class="text-emerald-500 mr-2">▹</span>
          {{ item }}
        </a>
      </div>
    </div>

  </nav>
</template>

<script>
export default {
  name: 'Navbar',

  props: {
    isDark: Boolean,  // mode nuit activé ou non
    lang: String,     // 'fr' ou 'en'
    t: Object,        // textes traduits
  },

  emits: ['toggleDark', 'toggleLang'],

  data() {
    return {
      activeSection: '',   // section actuellement visible
      hoveredItem: null,   // lien survolé par la souris
      scrolled: false,     // page scrollée ou non
      mobileOpen: false,   // menu mobile ouvert ou non
    }
  },

  computed: {
    // Liste des liens de navigation depuis les traductions
    navItems() {
      return [
        this.t.nav.about,
        this.t.nav.skills,
        this.t.nav.projects,
        this.t.nav.contact,
      ]
    },
  },

  mounted() {
    // On écoute le scroll de la page
    window.addEventListener('scroll', this.onScroll)
  },

  beforeUnmount() {
    // On enlève l'écouteur quand le composant est détruit
    window.removeEventListener('scroll', this.onScroll)
  },

  methods: {
    // Scroll fluide vers une section par son id
    scrollTo(item) {
      const ids = {
        [this.t.nav.about]: 'about',
        [this.t.nav.skills]: 'skills',
        [this.t.nav.projects]: 'projects',
        [this.t.nav.contact]: 'contact',
      }
      const el = document.getElementById(ids[item])
      if (el) el.scrollIntoView({ behavior: 'smooth' })
      this.mobileOpen = false
    },

    // Retour en haut de la page
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    },

    // Détecte quelle section est visible et met à jour activeSection
    onScroll() {
      // Détecte si la page est scrollée pour changer le style navbar
      this.scrolled = window.scrollY > 20

      const sections = {
        [this.t.nav.about]: document.getElementById('about'),
        [this.t.nav.skills]: document.getElementById('skills'),
        [this.t.nav.projects]: document.getElementById('projects'),
        [this.t.nav.contact]: document.getElementById('contact'),
      }

      for (const key in sections) {
        const el = sections[key]
        if (!el) continue
        const rect = el.getBoundingClientRect()
        if (rect.top <= 80 && rect.bottom >= 80) {
          this.activeSection = key
          break
        }
      }
    },
  },
}
</script>

<style scoped>
/* Animation de rotation lente pour le cercle autour de la photo */
@keyframes spin-slow {
  from { transform: rotate(0deg) scale(1.1); }
  to   { transform: rotate(360deg) scale(1.1); }
}
.animate-spin-slow {
  animation: spin-slow 3s linear infinite;
}
</style>