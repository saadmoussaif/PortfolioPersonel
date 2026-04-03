<template>
  <section id="contact"
           class="py-24 px-6 bg-gradient-to-b from-blue-950 to-blue-900
                  relative overflow-hidden text-white min-h-screen
                  flex items-center">

    <!-- ─── FOND DÉCORATIF ────────────────────────────────── -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-1/4 left-1/4 w-96 h-96 rounded-full
                  bg-emerald-500/5 blur-3xl"></div>
      <div class="absolute bottom-1/4 right-1/4 w-80 h-80 rounded-full
                  bg-blue-400/5 blur-3xl"></div>
      <!-- Grille décorative -->
      <div class="absolute inset-0 opacity-5"
           style="background-image: linear-gradient(rgba(255,255,255,.1) 1px, transparent 1px),
                                    linear-gradient(90deg, rgba(255,255,255,.1) 1px, transparent 1px);
                  background-size: 60px 60px;">
      </div>
    </div>

    <div class="max-w-4xl mx-auto relative z-10 w-full">

      <!-- ─── TITRE ──────────────────────────────────────── -->
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-6xl font-bold text-white mb-6">
          {{ t.contact.title }}
        </h2>
        <p class="text-blue-300/70 text-lg max-w-lg mx-auto">
          {{ t.contact.desc }}
        </p>
        <!-- Ligne décorative -->
        <div class="mt-6 flex justify-center">
          <div class="h-0.5 w-16 bg-gradient-to-r from-emerald-400 to-blue-400 rounded-full"></div>
        </div>
      </div>

      <!-- ─── LIENS DE CONTACT ───────────────────────────── -->
      <div class="flex flex-col gap-5 max-w-xl mx-auto">

        <a v-for="(link, index) in links"
           :key="link.label"
           :href="link.href"
           target="_blank"
           class="group relative inline-flex items-center gap-4 px-6 py-3 rounded-xl
                  border border-blue-700/20
                  bg-blue-900/25 backdrop-blur-sm
                  hover:border-cyan-300/90
                  hover:bg-gradient-to-r hover:from-blue-700 hover:via-blue-600 hover:to-cyan-500/40
                  hover:-translate-y-1 hover:scale-105
                  hover:shadow-2xl
                  transition-all duration-300 ease-out overflow-hidden link-hover-effect"
           style="margin-right: 16px;"           :style="{
             opacity: visible ? 1 : 0,
             transform: visible ? 'translateY(0)' : 'translateY(40px)',
             transition: 'all 0.6s ease-out',
             transitionDelay: index * 150 + 'ms'
           }"
           :class="link.hoverClass">

          <!-- Fond coloré qui glisse au hover -->
          <div class="absolute inset-0 opacity-0 group-hover:opacity-100
                      transition-opacity duration-400 rounded-2xl"
               :class="link.bgClass"></div>

          <!-- Ligne colorée à gauche -->
          <div class="absolute left-0 top-0 bottom-0 w-0.5 rounded-l-2xl
                      scale-y-0 group-hover:scale-y-100
                      transition-transform duration-400 origin-bottom"
               :class="link.lineClass"></div>

          <!-- Icône / Logo -->
          <div class="relative z-10 w-14 h-14 rounded-xl flex items-center justify-center
                      border border-blue-700/50 bg-blue-800/50
                      group-hover:scale-110 group-hover:rotate-3
                      group-hover:border-white/20 group-hover:bg-white/10
                      transition-all duration-300 flex-shrink-0"
               :class="link.iconHoverClass">
            <img :src="'/' + link.icon"
                 :alt="link.label"
                 class="w-8 h-8 object-contain transition-all duration-300"
                 :class="[link.imgClass, link.imgHoverClass]"
                 @error="(e) => e.target.style.display='none'" />
          </div>

          <!-- Texte -->
          <div class="relative z-10 flex-1">
            <div class="font-mono text-xs text-blue-400 mb-1
                        group-hover:text-white/60 transition-colors duration-300">
              {{ link.label }}
            </div>
            <div class="text-white font-medium text-sm
                        group-hover:text-white transition-colors duration-300">
              {{ link.value }}
            </div>
          </div>

          <!-- Flèche animée à droite -->
          <div class="relative z-10 text-blue-600
                      group-hover:text-emerald-400
                      transition-all duration-300
                      translate-x-0 group-hover:translate-x-2
                      opacity-0 group-hover:opacity-100 text-xl">
            →
          </div>

          <!-- Particules qui apparaissent au hover -->
          <div class="absolute top-2 right-4 w-1.5 h-1.5 rounded-full
                      bg-emerald-400 opacity-0 group-hover:opacity-100
                      group-hover:animate-ping transition-opacity duration-300"></div>
          <div class="absolute bottom-3 right-10 w-1 h-1 rounded-full
                      bg-blue-300 opacity-0 group-hover:opacity-60
                      transition-opacity duration-500"
               style="transition-delay: 100ms;"></div>

        </a>

      </div>

      <!-- ─── MESSAGE BAS DE PAGE ───────────────────────── -->
      <div class="text-center mt-16">
        <p class="font-mono text-xs text-blue-500">
          Réponse garantie sous 24h · Response guaranteed within 24h
        </p>
        <div class="mt-4 flex justify-center items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
          
        </div>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'ContactSection',
  props: { t: Object },

  data() {
    return {
      // Contrôle l'animation d'entrée
      visible: false,

      links: [
        {
          label: 'Email',
          value: 'moussaifsaad4@gmail.com',
          href: 'mailto:moussaifsaad4@gmail.com',
          icon: 'gmail.png',
          imgClass: '',
          imgHoverClass: 'group-hover:animate-bounce',
          iconHoverClass: 'group-hover:animate-shake',
          // Couleur rouge Gmail au hover
          bgClass: 'bg-red-500/8',
          lineClass: 'bg-red-400',
          hoverClass: 'hover:shadow-red-500/10',
        },
        {
          label: 'GitHub',
          value: 'github.com/saadmoussaif',
          href: 'https://github.com/saadmoussaif',
          icon: 'github.png',
          imgClass: 'opacity-80',
          imgHoverClass: 'group-hover:drop-shadow-lg group-hover:brightness-110 group-hover:opacity-100 github-glow',
          iconHoverClass: 'group-hover:animate-glow',
          // Couleur grise GitHub au hover
          bgClass: 'bg-white/5',
          lineClass: 'bg-gray-300',
          hoverClass: 'hover:shadow-gray-500/10',
        },
        {
          label: 'LinkedIn',
          value: 'linkedin.com/in/saad-moussaif',
          href: 'https://www.linkedin.com/in/saad-moussaif-369182226/',
          icon: 'linkdin.png',
          imgClass: '',
          imgHoverClass: 'group-hover:rotate-12 group-hover:scale-125',
          iconHoverClass: 'group-hover:animate-float',
          // Couleur bleue LinkedIn au hover
          bgClass: 'bg-blue-400/10',
          lineClass: 'bg-blue-400',
          hoverClass: 'hover:shadow-blue-400/15',
        },
      ],
    }
  },

  mounted() {
    // Animation réactivable à chaque scroll entrer/sortir
    const observer = new IntersectionObserver(
      (entries) => {
        const isVisible = entries.some(entry => entry.isIntersecting)
        this.visible = isVisible
      },
      { threshold: 0.25 }
    )
    observer.observe(this.$el)
  },
}
</script>

<style scoped>
/* Animations avancées pour les liens */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  10%, 30%, 50%, 70%, 90% { transform: translateX(-2px); }
  20%, 40%, 60%, 80% { transform: translateX(2px); }
}

@keyframes glow {
  0%, 100% { box-shadow: 0 0 5px rgba(168, 85, 247, 0.4); }
  50% { box-shadow: 0 0 20px rgba(168, 85, 247, 0.8), 0 0 30px rgba(168, 85, 247, 0.4); }
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-5px); }
}

.animate-shake:hover {
  animation: shake 0.5s ease-in-out;
}

.animate-glow:hover {
  animation: glow 2s ease-in-out infinite;
}

.animate-float:hover {
  animation: float 1s ease-in-out infinite;
}

/* Amélioration de l'animation bounce pour Gmail */
.group:hover .animate-bounce {
  animation: bounce 0.6s ease-in-out;
}

/* Style spécial pour GitHub */
.github-glow:hover {
  filter: drop-shadow(0 0 10px rgba(255, 255, 255, 0.8));
}

/* Animation globale de hover LINK */
.link-hover-effect:hover {
  background-image: linear-gradient(90deg, rgba(56, 189, 248, 0.35), rgba(14, 165, 233, 0.25));
  border-color: rgba(56, 189, 248, 0.8);
  box-shadow: 0 18px 30px rgba(14, 165, 233, 0.25);
}

.link-hover-effect:hover .relative.z-10 {
  transform: translateY(-1px) scale(1.04);
}
</style>