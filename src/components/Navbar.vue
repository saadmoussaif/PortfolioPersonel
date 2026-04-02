<template>
  <nav :class="[
    'fixed top-0 left-0 right-0 z-50 transition-all duration-500',
    scrolled
      ? 'bg-blue-950/95 backdrop-blur-lg shadow-lg shadow-blue-950/50 border-b border-blue-800/50'
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

      <!-- NAV LINKS -->
      <div class="hidden md:flex items-center gap-2 relative">

        <!-- UNDERLINE ANIMÉE -->
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

          <!-- BACKGROUND HOVER -->
          <span :class="[
            'absolute inset-0 rounded-lg transition-all duration-300',
            hoveredItem === item && activeSection !== item
              ? 'bg-blue-800/40 opacity-100 scale-100'
              : 'bg-blue-800/0 opacity-0 scale-95'
          ]"></span>

          <!-- CONTENT -->
          <span class="relative z-10 flex items-center gap-1.5">

            <!-- ICON -->
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

      <!-- RIGHT BUTTONS -->
      <div class="flex items-center gap-3">

        <!-- LANGUAGE DROPDOWN -->
        <div class="relative">

          <button 
            @click="open = !open"
            class="font-mono text-xs px-3 py-1.5 
                   border-2 border-white 
                   text-gray-300 
                   hover:border-emerald-400 hover:text-emerald-400
                   rounded">

            {{ lang === 'fr' ? 'FR' : 'EN' }}

          </button>

          <div v-if="open"
               class="absolute right-0 mt-2 w-32 bg-blue-950 border border-blue-700 rounded-lg shadow-lg z-50 p-2 space-y-2">

            <!-- FR -->
            <div 
              @click="changeLang('fr')"
              class="flex items-center justify-between cursor-pointer px-2 py-1 hover:bg-blue-800 rounded">

              <span class="text-gray-300 text-sm">Français</span>

              <span class="border border-white px-2 py-0.5 text-xs text-gray-300 rounded">
                FR
              </span>

            </div>

            <!-- EN -->
            <div 
              @click="changeLang('en')"
              class="flex items-center justify-between cursor-pointer px-2 py-1 hover:bg-blue-800 rounded">

              <span class="text-gray-300 text-sm">English</span>

              <span class="border border-white px-2 py-0.5 text-xs text-gray-300 rounded">
                EN
              </span>

            </div>

          </div>

        </div>

        <!-- DARK MODE -->
        <button @click="$emit('toggleDark')"
                class="w-9 h-9 rounded-full flex items-center justify-center border border-blue-600 text-gray-200 hover:border-emerald-400">
          {{ isDark ? '☀️' : '🌙' }}
        </button>

      </div>

    </div>

  </nav>
</template>

<script>
export default {
  name: 'Navbar',

  props: {
    isDark: Boolean,
    lang: String,
    t: Object,
  },

  emits: ['toggleDark', 'toggleLang'],

  data() {
    return {
      activeSection: '',
      hoveredItem: null,
      scrolled: false,
      open: false,

      itemRefs: [],
      indicatorStyle: {}
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
    }
  },

  mounted() {
    window.addEventListener('scroll', this.onScroll)

    this.$nextTick(() => {
      this.updateIndicator()
    })
  },

  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  },

  methods: {

    setItemRef(el) {
      if (el) this.itemRefs.push(el)
    },

    updateIndicator() {
      const index = this.navItems.findIndex(item => item === this.activeSection)
      const el = this.itemRefs[index]

      if (el) {
        this.indicatorStyle = {
          width: el.offsetWidth + 'px',
          transform: `translateX(${el.offsetLeft}px)`
        }
      }
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

      this.open = false
    },

    scrollToTop() {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    },

    onScroll() {
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

      this.updateIndicator()
    },

    changeLang(l) {
      if (this.lang === l) {
        this.open = false
        return
      }

      this.$emit('toggleLang', l)
      this.open = false
    }
  }
}
</script>