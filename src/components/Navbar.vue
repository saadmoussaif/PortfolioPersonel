<template>
  <nav :class="[
    'fixed top-0 left-0 right-0 z-50 transition-all duration-500',
    scrolled
      ? 'bg-blue-950/95 backdrop-blur-lg shadow-lg border-b border-blue-800/50'
      : 'bg-blue-900/90 backdrop-blur-md border-b border-blue-800/30'
  ]">

    <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">

      <!-- LOGO -->
      <div class="flex items-center gap-3">
        <div class="relative w-10 h-10 flex items-center justify-center">
          <div class="absolute inset-0 rounded-full bg-emerald-400 blur-md opacity-40"></div>
          <div class="relative w-10 h-10 rounded-full flex items-center justify-center
                      bg-gradient-to-br from-emerald-400 to-blue-500
                      text-white font-bold text-sm shadow-lg">
            SM
          </div>
        </div>

        <span class="font-mono font-bold text-lg cursor-pointer" @click="scrollToTop">
          <span class="text-emerald-400">SAAD</span>
          <span class="text-blue-400">dev</span>
        </span>
      </div>

      <!-- DESKTOP NAV -->
      <div class="hidden md:flex items-center gap-2 relative">

        <span
          class="absolute bottom-0 h-0.5 bg-emerald-400 transition-all duration-300"
          :style="indicatorStyle">
        </span>

        <a v-for="item in navItems"
           :key="item"
           :ref="setItemRef"
           @click="scrollTo(item)"
           @mouseenter="hoveredItem = item"
           @mouseleave="hoveredItem = null"
           :class="[
             'relative px-4 py-2 text-sm font-mono cursor-pointer rounded-lg transition-all duration-300',
             activeSection === item
               ? 'text-emerald-400 bg-blue-800/60'
               : 'text-gray-300 hover:text-white'
           ]">

          <span :class="[
            'absolute inset-0 rounded-lg transition-all duration-300',
            hoveredItem === item && activeSection !== item
              ? 'bg-blue-800/40 opacity-100 scale-100'
              : 'bg-blue-800/0 opacity-0 scale-95'
          ]"></span>

          <span class="relative z-10 flex items-center gap-1.5">

            <span class="text-emerald-400 text-xs transition-all duration-300"
                  :class="hoveredItem === item || activeSection === item
                    ? 'opacity-100 translate-x-0'
                    : 'opacity-0 -translate-x-2'">
              ▹
            </span>

            {{ item }}

          </span>

        </a>

      </div>

      <!-- RIGHT -->
      <div class="flex items-center gap-3">

        <!-- LANG -->
        <div class="relative">

          <button 
            @click="openLang = !openLang"
            class="font-mono text-xs px-3 py-1.5 
                   border-2 border-white 
                   text-gray-300 
                   hover:border-emerald-400 hover:text-emerald-400
                   rounded">
            {{ lang === 'fr' ? 'FR' : 'EN' }}
          </button>

          <div v-if="openLang"
               class="absolute right-0 mt-2 w-32 bg-blue-950 border border-blue-700 rounded-lg shadow-lg z-50 p-2 space-y-2">

            <div 
              @click="changeLang('fr')"
              class="flex items-center justify-between cursor-pointer px-2 py-1 hover:bg-blue-800 rounded">
              <span class="text-gray-300 text-sm">Français</span>
              <span class="border border-white px-2 py-0.5 text-xs text-gray-300 rounded">FR</span>
            </div>

            <div 
              @click="changeLang('en')"
              class="flex items-center justify-between cursor-pointer px-2 py-1 hover:bg-blue-800 rounded">
              <span class="text-gray-300 text-sm">English</span>
              <span class="border border-white px-2 py-0.5 text-xs text-gray-300 rounded">EN</span>
            </div>

          </div>

        </div>

        <!-- MOBILE BUTTON -->
        <button @click="toggleMenu"
                class="md:hidden text-white text-2xl">
          ☰
        </button>

      </div>

    </div>

    <!-- OVERLAY -->
    <div v-if="menuOpen"
         @click="toggleMenu"
         class="fixed inset-0 bg-black/50 backdrop-blur-sm z-40 transition-opacity duration-300">
    </div>

    <!-- MOBILE MENU -->
    <div :class="[
      'fixed top-4 right-4 h-[calc(100%-2rem)] w-1/2 max-w-sm z-50',
      'bg-[#2c2c2c]/95 backdrop-blur-xl',
      'border border-gray-500/30',
      'rounded-2xl',
      'shadow-2xl shadow-black/40',
      'transform transition-all duration-500 ease-in-out',
      menuOpen ? 'translate-x-0 opacity-100' : 'translate-x-full opacity-0'
    ]">

      <div class="flex justify-between items-center p-5 border-b border-gray-600/30">
        <span class="text-white font-semibold">Menu</span>
        <button @click="toggleMenu" class="text-white text-xl">✕</button>
      </div>

      <div class="flex flex-col gap-4 p-6">

        <a v-for="item in navItems"
           :key="item"
           @click="handleMobileClick(item)"
           class="flex items-center gap-3 text-gray-300 text-base 
                  hover:text-white hover:bg-white/5 px-3 py-2 rounded-lg 
                  transition cursor-pointer">

          <span class="w-2 h-2 bg-gray-400 rounded-full"></span>

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
    lang: String,
    t: Object,
  },

  emits: ['toggleLang'],

  data() {
    return {
      scrolled: false,
      menuOpen: false,
      openLang: false,
      activeSection: '',
      hoveredItem: null,
      itemRefs: {}
    }
  },

  computed: {
    navItems() {
      return [
        this.t.nav.about,
        this.t.nav.skills,
        this.t.nav.projects,
        this.t.nav.contact,
      ]
    },
    indicatorStyle() {
      const activeRef = this.itemRefs[this.activeSection]
      if (!activeRef) return { width: '0px', left: '0px' }
      return {
        width: activeRef.offsetWidth + 'px',
        left: activeRef.offsetLeft + 'px'
      }
    }
  },

  mounted() {
    window.addEventListener('scroll', this.onScroll)
  },

  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  },

  methods: {

    toggleMenu() {
      this.menuOpen = !this.menuOpen
    },

    handleMobileClick(item) {
      this.scrollTo(item)
      this.menuOpen = false
    },

    changeLang(l) {
      if (this.lang === l) {
        this.openLang = false
        return
      }
      this.$emit('toggleLang', l)
      this.openLang = false
    },

    scrollTo(item) {
      const ids = {
        [this.t.nav.about]: 'about',
        [this.t.nav.skills]: 'skills',
        [this.t.nav.projects]: 'projects',
        [this.t.nav.contact]: 'contact',
      }

      const el = document.getElementById(ids[item])
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },

    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    },

    setItemRef(el) {
      if (el) {
        this.itemRefs[el.textContent.trim()] = el
      }
    },

    updateActiveSection() {
      const ids = {
        [this.t.nav.about]: 'about',
        [this.t.nav.skills]: 'skills',
        [this.t.nav.projects]: 'projects',
        [this.t.nav.contact]: 'contact',
      }

      for (const [name, id] of Object.entries(ids)) {
        const el = document.getElementById(id)
        if (el) {
          const rect = el.getBoundingClientRect()
          if (rect.top <= 100 && rect.bottom >= 100) {
            this.activeSection = name
            return
          }
        }
      }
    },

    onScroll() {
      this.scrolled = window.scrollY > 20
      this.updateActiveSection()
    }

  }
}
</script>