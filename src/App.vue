<template>
  <div :class="isDark ? 'dark' : ''" class="min-h-screen">
    <div class="bg-white dark:bg-gray-950 text-gray-900 dark:text-white transition-colors duration-300">

      <!-- Navbar : on lui passe la langue et le mode nuit -->
      <Navbar
        :isDark="isDark"
        :lang="lang"
        :t="t"
        @toggleDark="toggleDark"
        @toggleLang="toggleLang"
      />

      <!-- Sections du portfolio -->
      <HeroSection :t="t" />
      <AboutSection :t="t" />
      <SkillsSection :t="t" />
      <ProjectsSection :t="t" />
      <ContactSection :t="t" />
      <fotterSection :t="t" />

    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'
import fotterSection from './components/fotterSection.vue'
import { translations } from './translations'

export default {
  name: 'App',
  components: { Navbar, HeroSection, AboutSection, SkillsSection, ProjectsSection, ContactSection, fotterSection },
  data() {
    return {
      isDark: false,
      lang: 'fr',
    }
  },
  computed: {
    t() {
      return translations[this.lang]
    }
  },
  methods: {
    toggleDark() {
      this.isDark = !this.isDark
    },
    toggleLang() {
      this.lang = this.lang === 'fr' ? 'en' : 'fr'
    }
  }
}
</script>