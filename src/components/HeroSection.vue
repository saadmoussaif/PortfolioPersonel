<template>
  <!-- Section héro : première chose visible sur la page -->
  <section class="min-h-screen flex items-center
                  pt-20 pb-12 px-6
                  bg-gradient-to-br from-blue-950 via-blue-900 to-blue-950
                  relative overflow-hidden">

    <!-- ─── FOND ANIMÉ (cercles décoratifs) ──────────────── -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden">
      <!-- Grand cercle flou en haut à droite -->
      <div class="absolute -top-32 -right-32 w-96 h-96 rounded-full
                  bg-emerald-500/10 blur-3xl animate-pulse"></div>
      <!-- Cercle bleu en bas à gauche -->
      <div class="absolute -bottom-20 -left-20 w-80 h-80 rounded-full
                  bg-blue-400/10 blur-3xl animate-pulse"
           style="animation-delay: 1s;"></div>
      <!-- Petits points décoratifs -->
      <div class="absolute top-1/4 left-1/4 w-1 h-1 rounded-full bg-emerald-400/40"></div>
      <div class="absolute top-1/3 right-1/3 w-1.5 h-1.5 rounded-full bg-blue-300/30"></div>
      <div class="absolute bottom-1/3 left-1/2 w-1 h-1 rounded-full bg-emerald-300/40"></div>
    </div>

    <div class="max-w-6xl mx-auto w-full relative z-10">

      <!-- ─── LAYOUT : TEXTE À GAUCHE, PHOTO À DROITE ──── -->
      <div class="flex flex-col-reverse md:flex-row items-center
                  justify-between gap-12">

        <!-- ── COLONNE GAUCHE : TEXTE ──────────────────── -->
        <div class="flex-1 text-center md:text-left">

          <!-- Badge disponible -->
          <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full
                      bg-emerald-500/10 border border-emerald-500/30
                      text-emerald-400 text-xs font-mono mb-8
                      animate-fade-in">
            <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
            Disponible · Available
          </div>

          <!-- Bonjour -->
          <p class="text-blue-300 font-mono text-lg mb-2 animate-slide-up"
             style="animation-delay: 0.1s;">
            {{ t.hero.greeting }}
          </p>

          <!-- Nom principal -->
          <h1 class="text-5xl md:text-7xl font-bold mb-4 leading-none tracking-tight
                     text-white animate-slide-up"
              style="animation-delay: 0.2s;">
            MOUSSAIF<br>
            <span class="text-transparent bg-clip-text
                         bg-gradient-to-r from-emerald-400 to-blue-400">
              SAAD
            </span>
          </h1>

          <!-- Titre poste -->
          <h2 class="text-lg md:text-xl text-emerald-400 font-mono mb-6
                     animate-slide-up" style="animation-delay: 0.3s;">
            {{ t.hero.title }}
          </h2>

          <!-- Description -->
          <p class="text-blue-200/70 text-base max-w-lg mb-10 leading-relaxed
                    animate-slide-up" style="animation-delay: 0.4s;">
            {{ t.hero.desc }}
          </p>

          <!-- Boutons CTA -->
          <div class="flex gap-4 justify-center md:justify-start flex-wrap
                      animate-slide-up" style="animation-delay: 0.5s;">

            <!-- Bouton principal -->
            <button @click="scrollTo('projects')"
                    class="group px-8 py-3 rounded-lg font-mono text-sm
                           bg-emerald-500 hover:bg-emerald-400 text-blue-950
                           font-bold transition-all duration-300
                           hover:-translate-y-1
                           hover:shadow-xl hover:shadow-emerald-500/30
                           flex items-center gap-2">
              {{ t.hero.cta }}
              <span class="transition-transform duration-300 group-hover:translate-x-1">→</span>
            </button>

            <!-- Bouton secondaire -->
            <button @click="scrollTo('contact')"
                    class="px-8 py-3 rounded-lg font-mono text-sm
                           border border-blue-500/50 text-blue-200
                           hover:border-emerald-400 hover:text-emerald-400
                           hover:bg-emerald-400/5
                           transition-all duration-300 hover:-translate-y-1">
              {{ t.hero.contact }}
            </button>

          </div>

          <!-- Stats -->
          <div class="flex gap-10 mt-14 justify-center md:justify-start
                      animate-slide-up" style="animation-delay: 0.6s;">
            <div v-for="stat in stats" :key="stat.label" class="text-center md:text-left">
              <div class="text-3xl font-bold text-emerald-400">
                {{ stat.value }}
              </div>
              <div class="text-xs font-mono text-blue-300/60 mt-1">
                {{ stat.label }}
              </div>
            </div>
          </div>

        </div>

        <!-- ── COLONNE DROITE : PHOTO ──────────────────── -->
        <div class="flex-shrink-0 flex items-center justify-center
                    animate-fade-in" style="animation-delay: 0.3s;">

          <div class="relative">

            <!-- Cercle qui tourne lentement autour de la photo -->
            <div class="absolute inset-0 rounded-full
                        bg-gradient-to-r from-emerald-400 via-blue-400 to-emerald-400
                        animate-spin-slow opacity-70 scale-105
                        blur-sm"></div>

            <!-- Deuxième cercle décoratif qui tourne en sens inverse -->
            <div class="absolute -inset-3 rounded-full
                        border border-emerald-400/20
                        animate-spin-reverse"></div>

            <!-- Troisième cercle pointillé -->
            <div class="absolute -inset-6 rounded-full
                        border border-dashed border-blue-400/20
                        animate-spin-slow"
                 style="animation-duration: 15s;"></div>

            <!-- Conteneur photo principal -->
            <div class="relative w-64 h-64 md:w-80 md:h-80 rounded-full
                        bg-gradient-to-br from-blue-800 to-blue-900
                        border-4 border-blue-700/50
                        overflow-hidden
                        hover:scale-105 transition-transform duration-500
                        cursor-pointer group z-10">

              <!-- ⚠️ REMPLACEZ src="/photo.jpg" PAR VOTRE VRAIE PHOTO -->
              <!-- Mettez votre photo dans le dossier public/ -->
              <img src="/public/saadM.jpeg"
                   alt="MOUSSAIF SAAD"
                   class="w-full h-full object-cover object-center
                          transition-transform duration-500
                          group-hover:scale-110"
                   @error="photoError = true"
                   v-if="!photoError" />

              <!-- Placeholder si pas de photo -->
              <div v-else
                   class="w-full h-full flex flex-col items-center justify-center
                          bg-gradient-to-br from-blue-800 to-blue-900">
                <span class="text-5xl font-bold text-emerald-400 mb-2">MS</span>
                <span class="text-xs font-mono text-blue-300/50">
                  Ajoutez photo.jpg<br>dans /public/
                </span>
              </div>

              <!-- Overlay au hover -->
              <div class="absolute inset-0 bg-emerald-500/10
                          opacity-0 group-hover:opacity-100
                          transition-opacity duration-300"></div>

            </div>

            <!-- Badge statut en bas de la photo -->
            <div class="absolute -bottom-3 left-1/2 -translate-x-1/2
                        bg-blue-900 border border-emerald-500/40
                        px-4 py-1.5 rounded-full
                        flex items-center gap-2 z-20
                        shadow-lg shadow-blue-950/50">
              <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
              <span class="font-mono text-xs text-emerald-400 whitespace-nowrap">
                Full Stack Engineer
              </span>
            </div>

            <!-- Points décoratifs autour de la photo -->
            <div class="absolute -top-2 -right-2 w-4 h-4 rounded-full
                        bg-emerald-400/60 animate-bounce z-20"
                 style="animation-delay: 0.5s;"></div>
            <div class="absolute -bottom-2 -left-2 w-3 h-3 rounded-full
                        bg-blue-400/60 animate-bounce z-20"
                 style="animation-delay: 1s;"></div>

          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',

  props: {
    t: Object, // textes traduits reçus depuis App.vue
  },

  data() {
    return {
      // Si true = la photo n'a pas pu charger → affiche les initiales MS
      photoError: false,

      // Statistiques affichées sous les boutons
      stats: [
        { value: '4+', label: 'Ans / Years' },
        { value: '12', label: 'Projets / Projects' },
        { value: '99%', label: 'Satisfaction' },
      ],
    }
  },

  methods: {
    // Scroll fluide vers une section
    scrollTo(id) {
      document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
    },
  },
}
</script>

<style scoped>
/* ── Animation : apparition en fondu ── */
@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.animate-fade-in {
  animation: fade-in 0.8s ease both;
}

/* ── Animation : glissement vers le haut ── */
@keyframes slide-up {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-slide-up {
  animation: slide-up 0.7s ease both;
}

/* ── Rotation lente pour le cercle autour de la photo ── */
@keyframes spin-slow {
  from { transform: rotate(0deg) scale(1.05); }
  to   { transform: rotate(360deg) scale(1.05); }
}
.animate-spin-slow {
  animation: spin-slow 8s linear infinite;
}

/* ── Rotation inverse pour le second cercle ── */
@keyframes spin-reverse {
  from { transform: rotate(360deg); }
  to   { transform: rotate(0deg); }
}
.animate-spin-reverse {
  animation: spin-reverse 12s linear infinite;
}
</style>