<template>
  <section id="about"
           class="py-24 px-6 bg-white dark:bg-gray-900 relative overflow-hidden">

    <!-- ─── FOND DÉCORATIF ────────────────────────────────── -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-0 right-0 w-96 h-96 rounded-full
                  bg-emerald-50 dark:bg-emerald-900/10 blur-3xl"></div>
      <div class="absolute bottom-0 left-0 w-72 h-72 rounded-full
                  bg-blue-50 dark:bg-blue-900/10 blur-3xl"></div>
    </div>

    <div class="max-w-6xl mx-auto relative z-10">

      <!-- ─── TITRE ─────────────────────────────────────── -->
      <div class="mb-16 text-center"
           :class="visible ? 'animate-fade-up' : 'opacity-0 translate-y-8'">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400
                  uppercase tracking-widest mb-3">
          {{ t.about.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white">
          {{ t.about.title }}
        </h2>
        <div class="mt-4 flex justify-center">
          <div class="h-0.5 bg-gradient-to-r from-emerald-500 to-blue-500 rounded-full
                      transition-all duration-700"
               :class="visible ? 'w-16' : 'w-0'"></div>
        </div>
      </div>

      <!-- ─── CONTENU ───────────────────────────────────── -->
      <div class="grid md:grid-cols-2 gap-12 items-center">

        <!-- ── GAUCHE ──────────────────────────────────── -->
        <div>

          <!-- Texte -->
          <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed mb-10
                    transition-all duration-700"
             :class="visible ? 'opacity-100 translate-x-0' : 'opacity-0 -translate-x-10'">
            {{ t.about.desc }}
          </p>

          <!-- ── CARTES STATS ── -->
          <div class="grid grid-cols-3 gap-4 mb-10">
            <div v-for="(stat, i) in stats" :key="stat.label"
                 class="group relative bg-gray-50 dark:bg-gray-800 rounded-xl p-5
                        border border-gray-200 dark:border-gray-700 text-center
                        cursor-default overflow-hidden
                        hover:border-emerald-400 hover:-translate-y-3 hover:scale-105
                        hover:shadow-2xl hover:shadow-emerald-500/20
                        transition-all duration-400"
                 :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'"
                 :style="{ transitionDelay: (0.2 + i * 0.12) + 's', transitionDuration: '0.6s' }">

              <!-- Fond animé hover -->
              <div class="absolute inset-0 bg-gradient-to-br from-emerald-500/10 to-blue-500/5
                          opacity-0 group-hover:opacity-100 transition-opacity duration-400"></div>

              <!-- Ligne verte haut hover -->
              <div class="absolute top-0 left-0 right-0 h-0.5
                          bg-gradient-to-r from-emerald-400 to-blue-400
                          scale-x-0 group-hover:scale-x-100
                          transition-transform duration-400 origin-left"></div>

              <div class="relative z-10">
                <div class="text-2xl font-bold text-emerald-600 dark:text-emerald-400
                            group-hover:scale-125 transition-transform duration-300">
                  {{ stat.value }}
                </div>
                <div class="text-xs font-mono text-gray-400 mt-1
                            group-hover:text-gray-600 dark:group-hover:text-gray-200
                            transition-colors duration-300">
                  {{ stat.label }}
                </div>
              </div>
            </div>
          </div>

          <!-- ── BOUTON CV style contact-link ─────────────── -->
          <button @click="handleCVClick"
                  :style="{
                    opacity: visible ? 1 : 0,
                    transform: visible ? 'translateY(0)' : 'translateY(20px)',
                    transition: 'all 0.6s ease 0.55s'
                  }"
                  :class="[
  'group relative flex items-center gap-4 px-6 py-4 rounded-2xl',
  'border font-mono text-sm overflow-hidden w-full max-w-xs',
  'hover:-translate-y-2 hover:scale-[1.03]',
  'hover:shadow-2xl transition-all duration-400 ease-out',

  // STYLE NORMAL + HOVER
  'border-emerald-300 dark:border-emerald-700/60 bg-white dark:bg-gray-800',
  'hover:border-emerald-400 hover:bg-emerald-500/10 hover:shadow-emerald-500/20',

  // APRÈS CLICK
  cvClicked && 'border-emerald-500 bg-emerald-500/20 shadow-lg shadow-emerald-500/30'
]"

            <!-- Fond vert qui glisse de gauche au hover -->
            <div class="absolute inset-0 bg-emerald-500/10
                        -translate-x-full group-hover:translate-x-0
                        transition-transform duration-500 ease-out rounded-2xl"></div>

            <!-- Ligne verte à gauche qui monte au hover -->
            <div class="absolute left-0 top-0 bottom-0 w-0.5 rounded-l-2xl bg-emerald-400
                        scale-y-0 group-hover:scale-y-100
                        transition-transform duration-400 origin-bottom"></div>

            <!-- Icône avec rotation + scale au hover -->
            <div class="relative z-10 w-12 h-12 rounded-xl flex items-center justify-center
                        border bg-emerald-50 dark:bg-emerald-900/30
                        transition-all duration-300
                        group-hover:scale-125 group-hover:rotate-12
                        group-hover:shadow-lg group-hover:shadow-emerald-500/30"
                 :class="cvClicked
                   ? 'border-emerald-400 bg-emerald-100 dark:bg-emerald-800/50'
                   : 'border-emerald-200 dark:border-emerald-700/50'">
              <span class="text-xl transition-all duration-300
                           group-hover:animate-bounce">
                {{ cvClicked ? '✅' : '📄' }}
              </span>
            </div>

            <!-- Texte -->
            <div class="relative z-10 flex-1 text-left">
              <div class="font-mono text-xs mb-0.5 transition-colors duration-300"
                   :class="cvClicked
                     ? 'text-emerald-600 dark:text-emerald-400'
                     : 'text-gray-400 group-hover:text-emerald-500'">
                {{ cvClicked ? 'Succès !' : 'Mon curriculum vitae' }}
              </div>
              <div class="font-bold text-sm transition-colors duration-300"
                   :class="cvClicked
                     ? 'text-emerald-700 dark:text-emerald-300'
                     : 'text-gray-700 dark:text-gray-200 group-hover:text-emerald-600 dark:group-hover:text-emerald-400'">
                {{ cvClicked ? 'CV Téléchargé !' : 'Télécharger CV' }}
              </div>
            </div>

            <!-- Flèche animée -->
            <div class="relative z-10 transition-all duration-300
                        opacity-0 group-hover:opacity-100
                        translate-x-0 group-hover:translate-x-1"
                 :class="cvClicked ? 'text-emerald-500 opacity-100' : 'text-emerald-400'">
              {{ cvClicked ? '✓' : '→' }}
            </div>

            <!-- Particule ping coin haut droite -->
            <div class="absolute top-2 right-3 w-1.5 h-1.5 rounded-full bg-emerald-400
                        opacity-0 group-hover:opacity-100 group-hover:animate-ping
                        transition-opacity duration-300"></div>

          </button>

        </div>

        <!-- ── DROITE : CARTE PROFIL ──────────────────── -->
        <div class="relative"
             :class="visible ? 'opacity-100 translate-x-0' : 'opacity-0 translate-x-10'"
             style="transition: all 0.7s ease 0.25s">

          <!-- Carte principale — slow motion scale au hover -->
          <div class="group bg-white dark:bg-gray-800 rounded-2xl p-8
                      border border-gray-200 dark:border-gray-700
                      shadow-xl shadow-gray-100 dark:shadow-none
                      hover:scale-[1.04] hover:-translate-y-3
                      hover:shadow-2xl hover:shadow-emerald-500/20
                      hover:border-emerald-300 dark:hover:border-emerald-500/40
                      transition-all duration-700 ease-in-out
                      relative overflow-hidden cursor-default">

            <!-- Fond subtil hover -->
            <div class="absolute inset-0 bg-gradient-to-br from-emerald-500/4 to-blue-500/3
                        opacity-0 group-hover:opacity-100 transition-opacity duration-700"></div>

            <!-- Ligne colorée en haut hover -->
            <div class="absolute top-0 left-0 right-0 h-0.5
                        bg-gradient-to-r from-emerald-400 via-blue-400 to-emerald-400
                        scale-x-0 group-hover:scale-x-100
                        transition-transform duration-700 origin-left"></div>

            <!-- ── Avatar + nom ──────────────────────────── -->
            <div class="flex items-center gap-4 mb-8 pb-6
                        border-b border-gray-100 dark:border-gray-700 relative z-10">

              <div class="relative">
                <div class="w-16 h-16 rounded-full overflow-hidden
                            border-2 border-emerald-400
                            group-hover:border-emerald-300
                            group-hover:scale-110 group-hover:shadow-lg
                            group-hover:shadow-emerald-500/40
                            transition-all duration-500">
                  <img src="/saadAI.png" alt="MOUSSAIF SAAD"
                       class="w-full h-full object-cover
                              group-hover:scale-110 transition-transform duration-500"
                       @error="photoError = true"
                       v-if="!photoError" />
                  <div v-else class="w-full h-full bg-emerald-50 dark:bg-emerald-900/30
                                    flex items-center justify-center
                                    text-xl font-bold text-emerald-600">MS</div>
                </div>
                <!-- Point vert animé -->
                <div class="absolute -bottom-0.5 -right-0.5 w-4 h-4 rounded-full
                            bg-emerald-500 border-2 border-white dark:border-gray-800">
                  <div class="w-full h-full rounded-full bg-emerald-400 animate-ping opacity-75"></div>
                </div>
              </div>

              <div>
                <h3 class="font-bold text-gray-900 dark:text-white text-lg
                           group-hover:text-emerald-700 dark:group-hover:text-emerald-300
                           transition-colors duration-500">
                  MOUSSAIF SAAD
                </h3>
                <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400">
                  Full Stack Engineer
                </p>
              </div>
            </div>

            <!-- ── Lignes infos ───────────────────────────── -->
            <div class="space-y-2 relative z-10">
              <div v-for="(info, i) in infos" :key="info.label"
                   class="group/item flex items-center justify-between
                          py-2.5 px-3 rounded-lg cursor-default
                          border border-transparent
                          hover:bg-emerald-50 dark:hover:bg-emerald-900/20
                          hover:border-emerald-200 dark:hover:border-emerald-700/50
                          hover:translate-x-2
                          transition-all duration-300"
                   :style="{ transitionDelay: i * 40 + 'ms' }">

                <div class="flex items-center gap-2">
                  <span class="transition-transform duration-300
                               group-hover/item:scale-125 group-hover/item:rotate-12">
                    {{ info.icon }}
                  </span>
                  <span class="font-mono text-xs text-gray-400
                               group-hover/item:text-emerald-500
                               transition-colors duration-200">
                    {{ info.label }}
                  </span>
                </div>

                <span class="text-sm text-gray-700 dark:text-gray-300 font-medium
                             group-hover/item:text-emerald-600 dark:group-hover/item:text-emerald-400
                             transition-colors duration-200">
                  {{ info.value }}
                </span>

              </div>
            </div>

          </div>

          <!-- Ombre décorative derrière -->
          <div class="absolute -bottom-3 -right-3 w-full h-full rounded-2xl
                      bg-emerald-100 dark:bg-emerald-900/20
                      border border-emerald-200 dark:border-emerald-800/30
                      -z-10 transition-transform duration-700
                      group-hover:translate-x-1 group-hover:translate-y-1"></div>

        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',
  props: { t: Object },

  data() {
    return {
      photoError: false,
      visible: false,      // contrôle les animations d'entrée
      cvClicked: false,    // bouton CV cliqué → change couleur

      stats: [
        { value: '2+',  label: 'Ans / Years' },
        { value: '12',  label: 'Projets' },
        { value: '99%', label: 'Satisfaction' },
      ],

      infos: [
        { icon: '👤', label: 'Nom',      value: 'MOUSSAIF SAAD' },
        { icon: '💼', label: 'Poste',    value: 'Full Stack Engineer' },
        { icon: '📍', label: 'Location', value: 'Maroc' },
        { icon: '✉️', label: 'Email',    value: 'moussaifsaad4@gmail.com' },
        { icon: '✅', label: 'Statut',   value: 'Disponible' },
      ],
    }
  },

  mounted() {
    // ─── OBSERVER QUI SE RÉPÈTE ──────────────────────────
    // threshold: 0 → se déclenche dès qu'on entre/sort
    const observer = new IntersectionObserver(
      (entries) => {
        const entry = entries[0]
        if (entry.isIntersecting) {
          // Section visible → lance les animations
          setTimeout(() => { this.visible = true }, 80)
        } else {
          // Section hors vue → remet à zéro pour rejouer
          this.visible = false
        }
      },
      // threshold 0.1 = déclenche dès 10% visible
      { threshold: 0.1 }
    )
    // On n'appelle PAS observer.disconnect() → reste actif toujours
    observer.observe(this.$el)
  },

  methods: {
     handleCVClick() {
    this.cvClicked = true

    // Ouvre le CV dans un nouvel onglet
    window.open('/MOUSSAIF-SAADCV.pdf', '_blank')

    setTimeout(() => {
      this.cvClicked = false
    }, 2500)
  }
  },
}
</script>

<style scoped>
/* Animation fade + montée */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-fade-up {
  animation: fadeUp 0.6s ease both;
}
</style>