<template>
  <section id="projects"
           class="py-24 px-6 bg-gradient-to-b from-blue-950 to-blue-900 relative overflow-hidden">

    <!-- ─── FOND DÉCORATIF ────────────────────────────────── -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-20 right-10 w-72 h-72 rounded-full
                  bg-emerald-500/5 blur-3xl"></div>
      <div class="absolute bottom-10 left-10 w-60 h-60 rounded-full
                  bg-blue-400/5 blur-3xl"></div>
    </div>

    <div class="max-w-6xl mx-auto relative z-10">

      <!-- ─── TITRE ──────────────────────────────────────── -->
      <div class="mb-16 text-center"
           :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-8'"
           style="transition: all 0.6s ease">
        <p class="font-mono text-xs text-emerald-400 uppercase tracking-widest mb-3">
          {{ t.projects.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold text-white">
          {{ t.projects.title }}
        </h2>
        <div class="mt-4 flex justify-center">
          <div class="h-0.5 bg-gradient-to-r from-emerald-400 to-blue-400 rounded-full
                      transition-all duration-700"
               :class="visible ? 'w-16' : 'w-0'"></div>
        </div>
      </div>

      <!-- ─── GRILLE PROJETS ────────────────────────────── -->
      <div class="grid md:grid-cols-2 gap-6">

        <div v-for="(proj, i) in projects" :key="proj.title"
             class="group relative rounded-2xl p-6 cursor-pointer overflow-hidden
                    border transition-all duration-500 ease-out
                    hover:-translate-y-3 hover:scale-[1.02]
                    hover:shadow-2xl"
             :class="[
               visible
                 ? 'opacity-100 translate-y-0'
                 : 'opacity-0 translate-y-12',
               proj.borderClass,
               proj.hoverShadow,
             ]"
             :style="{
               transition: 'all 0.6s ease',
               transitionDelay: visible ? (i * 120) + 'ms' : '0ms',
               background: 'rgba(15, 23, 42, 0.7)',
             }"
             @mouseenter="hoveredCard = i"
             @mouseleave="hoveredCard = null">

          <!-- Fond coloré qui s'illumine au hover -->
          <div class="absolute inset-0 opacity-0 group-hover:opacity-100
                      transition-opacity duration-500 rounded-2xl"
               :class="proj.bgClass"></div>

          <!-- Ligne colorée en haut qui glisse au hover -->
          <div class="absolute top-0 left-0 right-0 h-0.5 rounded-t-2xl
                      scale-x-0 group-hover:scale-x-100
                      transition-transform duration-500 origin-left"
               :class="proj.lineClass"></div>

          <!-- Ligne colorée à gauche -->
          <div class="absolute left-0 top-0 bottom-0 w-0.5 rounded-l-2xl
                      scale-y-0 group-hover:scale-y-100
                      transition-transform duration-500 origin-top"
               :class="proj.lineClass"></div>

          <div class="relative z-10">

            <!-- ── EN-TÊTE : numéro + icône + flèche ─── -->
            <div class="flex justify-between items-start mb-5">
              <div class="flex items-center gap-3">
                <!-- Numéro avec fond coloré au hover -->
                <div class="w-10 h-10 rounded-xl flex items-center justify-center
                            border font-mono text-sm font-bold
                            transition-all duration-300
                            group-hover:scale-110 group-hover:rotate-3"
                     :class="[proj.numBg, proj.numText, proj.numBorder]">
                  {{ String(i+1).padStart(2,'0') }}
                </div>
                <!-- Icône projet -->
                <span class="text-2xl transition-all duration-300
                             group-hover:scale-125 group-hover:rotate-6">
                  {{ proj.icon }}
                </span>
              </div>

              <!-- Flèche animée -->
              <span class="text-xl transition-all duration-300
                           group-hover:-translate-y-1 group-hover:translate-x-1
                           group-hover:scale-125"
                    :class="hoveredCard === i ? proj.accentText : 'text-blue-700'">
                ↗
              </span>
            </div>

            <!-- ── TITRE ───────────────────────────────── -->
            <h3 class="text-xl font-bold mb-3 text-white
                       transition-colors duration-300"
                :class="hoveredCard === i ? proj.accentText : ''">
              {{ proj.title }}
            </h3>

            <!-- ── DESCRIPTION ────────────────────────── -->
            <p class="text-blue-300/70 text-sm leading-relaxed mb-5
                      group-hover:text-blue-200/90 transition-colors duration-300">
              {{ proj.desc }}
            </p>

            <!-- ── TAGS TECHNOLOGIES ───────────────────── -->
            <div class="flex flex-wrap gap-2 mb-4">
              <span v-for="tag in proj.tags" :key="tag"
                    class="px-3 py-1 text-xs font-mono rounded-lg
                           transition-all duration-300
                           group-hover:-translate-y-0.5 group-hover:scale-105
                           border"
                    :class="[proj.tagBg, proj.tagText, proj.tagBorder]">
                {{ tag }}
              </span>
            </div>

            <!-- ── MÉTRIQUES ───────────────────────────── -->
            <div class="flex gap-3 flex-wrap">
              <span v-for="m in proj.metrics" :key="m"
                    class="text-xs font-mono px-2 py-1 rounded-lg
                           border transition-all duration-300
                           group-hover:scale-105"
                    :class="[proj.metricText, proj.metricBorder]">
                {{ m }}
              </span>
            </div>

          </div>

          <!-- Particule ping au hover -->
          <div class="absolute top-3 right-3 w-2 h-2 rounded-full
                      opacity-0 group-hover:opacity-100
                      group-hover:animate-ping transition-opacity duration-300"
               :class="proj.pingColor"></div>

        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',
  props: { t: Object },

  data() {
    return {
      visible: false,
      hoveredCard: null,

      projects: [
        {
          title: 'SaaS Analytics Dashboard',
          desc: 'Tableau de bord temps réel pour une startup fintech. 50 000 utilisateurs actifs, latence < 200ms.',
          icon: '📊',
          tags: ['Vue.js', 'Node.js', 'WebSocket', 'PostgreSQL'],
          metrics: ['50k users', '< 200ms', '99.9% uptime'],
          // ── Couleurs ÉMERAUDE ──
          borderClass:  'border-emerald-900/50',
          hoverShadow:  'hover:shadow-emerald-500/20',
          bgClass:      'bg-gradient-to-br from-emerald-500/8 to-emerald-900/5',
          lineClass:    'bg-gradient-to-r from-emerald-400 to-emerald-600',
          accentText:   'text-emerald-400',
          numBg:        'bg-emerald-900/50 group-hover:bg-emerald-500/20',
          numText:      'text-emerald-400',
          numBorder:    'border-emerald-700/50 group-hover:border-emerald-400/60',
          tagBg:        'bg-emerald-900/30 group-hover:bg-emerald-500/20',
          tagText:      'text-emerald-300',
          tagBorder:    'border-emerald-700/40 group-hover:border-emerald-400/60',
          metricText:   'text-emerald-400',
          metricBorder: 'border-emerald-700/50 group-hover:border-emerald-400',
          pingColor:    'bg-emerald-400',
        },
        {
          title: 'API Microservices Platform',
          desc: 'Architecture distribuée pour une plateforme e-commerce sur AWS. Déploiement Kubernetes automatisé.',
          icon: '⚙️',
          tags: ['Python', 'Docker', 'Kubernetes', 'Redis'],
          metrics: ['12 services', 'AWS EKS', 'Auto-scaling'],
          // ── Couleurs BLEU ──
          borderClass:  'border-blue-800/50',
          hoverShadow:  'hover:shadow-blue-500/20',
          bgClass:      'bg-gradient-to-br from-blue-500/8 to-blue-900/5',
          lineClass:    'bg-gradient-to-r from-blue-400 to-blue-600',
          accentText:   'text-blue-400',
          numBg:        'bg-blue-900/50 group-hover:bg-blue-500/20',
          numText:      'text-blue-400',
          numBorder:    'border-blue-700/50 group-hover:border-blue-400/60',
          tagBg:        'bg-blue-900/30 group-hover:bg-blue-500/20',
          tagText:      'text-blue-300',
          tagBorder:    'border-blue-700/40 group-hover:border-blue-400/60',
          metricText:   'text-blue-400',
          metricBorder: 'border-blue-700/50 group-hover:border-blue-400',
          pingColor:    'bg-blue-400',
        },
        {
          title: 'Mobile App React Native',
          desc: 'Application cross-platform iOS/Android avec synchronisation offline-first et notifications push.',
          icon: '📱',
          tags: ['React Native', 'TypeScript', 'GraphQL'],
          metrics: ['10k+ DL', '4.8 ★', 'iOS & Android'],
          // ── Couleurs VIOLET ──
          borderClass:  'border-purple-800/50',
          hoverShadow:  'hover:shadow-purple-500/20',
          bgClass:      'bg-gradient-to-br from-purple-500/8 to-purple-900/5',
          lineClass:    'bg-gradient-to-r from-purple-400 to-purple-600',
          accentText:   'text-purple-400',
          numBg:        'bg-purple-900/50 group-hover:bg-purple-500/20',
          numText:      'text-purple-400',
          numBorder:    'border-purple-700/50 group-hover:border-purple-400/60',
          tagBg:        'bg-purple-900/30 group-hover:bg-purple-500/20',
          tagText:      'text-purple-300',
          tagBorder:    'border-purple-700/40 group-hover:border-purple-400/60',
          metricText:   'text-purple-400',
          metricBorder: 'border-purple-700/50 group-hover:border-purple-400',
          pingColor:    'bg-purple-400',
        },
        {
          title: 'DevOps Automation Tools',
          desc: 'Suite d\'outils CLI pour automatiser les déploiements et monitorer l\'infrastructure en temps réel.',
          icon: '🚀',
          tags: ['Python', 'Bash', 'Terraform', 'Prometheus'],
          metrics: ['-60% deploy time', 'Open source'],
          // ── Couleurs ORANGE ──
          borderClass:  'border-orange-800/50',
          hoverShadow:  'hover:shadow-orange-500/20',
          bgClass:      'bg-gradient-to-br from-orange-500/8 to-orange-900/5',
          lineClass:    'bg-gradient-to-r from-orange-400 to-orange-600',
          accentText:   'text-orange-400',
          numBg:        'bg-orange-900/50 group-hover:bg-orange-500/20',
          numText:      'text-orange-400',
          numBorder:    'border-orange-700/50 group-hover:border-orange-400/60',
          tagBg:        'bg-orange-900/30 group-hover:bg-orange-500/20',
          tagText:      'text-orange-300',
          tagBorder:    'border-orange-700/40 group-hover:border-orange-400/60',
          metricText:   'text-orange-400',
          metricBorder: 'border-orange-700/50 group-hover:border-orange-400',
          pingColor:    'bg-orange-400',
        },
      ],
    }
  },

  mounted() {
    // ── Observer qui se répète à chaque scroll ──
    // Pas de disconnect() → animation se rejoue à chaque fois
    const observer = new IntersectionObserver(
      (entries) => {
        const entry = entries[0]
        if (entry.isIntersecting) {
          // Visible → lance les animations
          setTimeout(() => { this.visible = true }, 80)
        } else {
          // Hors vue → remet à zéro pour rejouer
          this.visible = false
        }
      },
      { threshold: 0.1 }
    )
    observer.observe(this.$el)
  },
}
</script>