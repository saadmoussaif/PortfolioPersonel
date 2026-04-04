<template>
  <div :class="isDark ? 'dark' : ''" class="min-h-screen">
    <div class="bg-white dark:bg-gray-950 text-gray-900 dark:text-white
                transition-colors duration-300">

      <!-- ─── LOADING LANGUE ──────────────────────────── -->
      <!-- Apparaît 0.6s lors du changement de langue -->
      <LangLoader :show="langLoading" :from="lang" />

      <!-- ─── COMPOSANTS ─────────────────────────────── -->
      <Navbar
        :isDark="isDark"
        :lang="lang"
        :t="t"
        @toggleDark="isDark = !isDark"
        @toggleLang="handleToggleLang"
      />

      <HeroSection    :t="t" />
      <AboutSection   :t="t" />
      <SkillsSection  :t="t" />
      <ProjectsSection :t="t" />
      <ContactSection :t="t" />
      <FooterSection  :t="t" />

    </div>
  </div>
</template>

<script>
import Navbar           from './components/Navbar.vue'
import HeroSection      from './components/HeroSection.vue'
import AboutSection     from './components/AboutSection.vue'
import SkillsSection    from './components/SkillsSection.vue'
import ProjectsSection  from './components/ProjectsSection.vue'
import ContactSection   from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
import LangLoader from './components/Langloader.vue'


import { translations } from './translations.js'

export default {
  name: 'App',

  components: {
    Navbar, HeroSection, AboutSection, SkillsSection,
    ProjectsSection, ContactSection, FooterSection, LangLoader,
  },

  data() {
    return {
      isDark: false,
      lang: 'fr',
      langLoading: false, // contrôle l'affichage du loader
    }
  },

  computed: {
    t() {
      return translations[this.lang]
    },
  },

  methods: {
    // Changement de langue avec loading screen
    handleToggleLang() {
      // 1. Affiche le loader
      this.langLoading = true

      // 2. Change la langue après 600ms (pendant le loading)
      setTimeout(() => {
        this.lang = this.lang === 'fr' ? 'en' : 'fr'

        // 3. Cache le loader après encore 200ms
        setTimeout(() => {
          this.langLoading = false
        }, 200)

      }, 600)
    },
  },
}
</script>