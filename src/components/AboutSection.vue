<template>
  <section id="about"
           class="py-24 px-6 bg-white dark:bg-gray-900 relative overflow-hidden">

    <!-- Déco fond subtile -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-0 right-0 w-96 h-96 rounded-full
                  bg-emerald-50 dark:bg-emerald-900/10 blur-3xl"></div>
      <div class="absolute bottom-0 left-0 w-72 h-72 rounded-full
                  bg-blue-50 dark:bg-blue-900/10 blur-3xl"></div>
    </div>

    <div class="max-w-6xl mx-auto relative z-10">

      <!-- ─── TITRE ──────────────────────────────────────── -->
      <div class="mb-16 text-center">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400
                  uppercase tracking-widest mb-3">
          // {{ t.about.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white">
          {{ t.about.title }}
        </h2>
        <div class="mt-4 flex justify-center">
          <div class="h-0.5 w-16 bg-gradient-to-r from-emerald-500 to-blue-500 rounded-full"></div>
        </div>
      </div>

      <!-- ─── CONTENU ────────────────────────────────────── -->
      <div class="grid md:grid-cols-2 gap-12 items-center">

        <!-- GAUCHE : texte + stats + CV -->
        <div>
          <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed mb-10">
            {{ t.about.desc }}
          </p>

          <!-- Stats avec hover -->
          <div class="grid grid-cols-3 gap-4 mb-10">
            <div v-for="stat in stats" :key="stat.label"
                 class="group bg-gray-50 dark:bg-gray-800 rounded-xl p-5
                        border border-gray-200 dark:border-gray-700 text-center
                        hover:border-emerald-400 hover:-translate-y-2
                        hover:shadow-xl hover:shadow-emerald-500/15
                        transition-all duration-300 cursor-default">
              <div class="text-2xl font-bold text-emerald-600 dark:text-emerald-400
                          group-hover:scale-110 transition-transform duration-300">
                {{ stat.value }}
              </div>
              <div class="text-xs font-mono text-gray-400 mt-1">{{ stat.label }}</div>
            </div>
          </div>

          <!-- Bouton CV -->
          <a href="#"
             class="group inline-flex items-center gap-3 px-6 py-3 rounded-lg
                    border border-emerald-400 text-emerald-600 dark:text-emerald-400
                    hover:bg-emerald-500 hover:text-white hover:border-emerald-500
                    hover:-translate-y-1 hover:shadow-lg hover:shadow-emerald-500/25
                    transition-all duration-300 font-mono text-sm">
            <span>📄</span>
            Télécharger CV
            <span class="transition-transform duration-300 group-hover:translate-x-1">→</span>
          </a>
        </div>

        <!-- DROITE : carte profil -->
        <div class="relative">
          <div class="bg-white dark:bg-gray-800 rounded-2xl p-8
                      border border-gray-200 dark:border-gray-700
                      shadow-xl shadow-gray-100 dark:shadow-none
                      hover:shadow-2xl hover:shadow-emerald-500/10
                      hover:border-emerald-300 dark:hover:border-emerald-500/30
                      transition-all duration-500">

            <!-- Avatar + nom -->
            <div class="flex items-center gap-4 mb-8 pb-6
                        border-b border-gray-100 dark:border-gray-700">
              <div class="relative">
                <div class="w-16 h-16 rounded-full overflow-hidden border-2 border-emerald-400">
                  <img src="/public/saadAI.png" alt="MS"
                       class="w-full h-full object-cover"
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
                <h3 class="font-bold text-gray-900 dark:text-white text-lg">MOUSSAIF SAAD</h3>
                <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400">Full Stack Engineer</p>
              </div>
            </div>

            <!-- Infos avec hover -->
            <div class="space-y-2">
              <div v-for="info in infos" :key="info.label"
                   class="flex items-center justify-between py-2.5 px-3 rounded-lg
                          hover:bg-gray-50 dark:hover:bg-gray-700/50
                          border border-transparent
                          hover:border-gray-200 dark:hover:border-gray-600
                          transition-all duration-200 cursor-default group">
                <div class="flex items-center gap-2">
                  <span>{{ info.icon }}</span>
                  <span class="font-mono text-xs text-gray-400">{{ info.label }}</span>
                </div>
                <span class="text-sm text-gray-700 dark:text-gray-300
                             group-hover:text-emerald-600 dark:group-hover:text-emerald-400
                             transition-colors duration-200">
                  {{ info.value }}
                </span>
              </div>
            </div>
          </div>
          <!-- Ombre décorative derrière la carte -->
          <div class="absolute -bottom-3 -right-3 w-full h-full rounded-2xl
                      bg-emerald-100 dark:bg-emerald-900/20
                      border border-emerald-200 dark:border-emerald-800/30 -z-10"></div>
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
}
</script>