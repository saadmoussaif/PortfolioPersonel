<template>
  <section class="min-h-screen flex items-center
                  pt-32 pb-12 px-6
                  bg-gradient-to-br from-blue-950 via-blue-900 to-blue-950
                  relative overflow-hidden">

    <!-- ─── CURSEUR PERSONNALISÉ ──────────────────────────── -->
    <div class="cursor-dot"
         :style="{ left: cursor.x + 'px', top: cursor.y + 'px' }"></div>
    <div class="cursor-ring"
         :style="{ left: cursor.rx + 'px', top: cursor.ry + 'px' }"></div>

    <!-- ─── CANVAS 3D PARTICULES ─────────────────────────── -->
    <canvas ref="canvas3d"
            class="absolute inset-0 w-full h-full pointer-events-none z-0">
    </canvas>

    <!-- ─── FOND DÉCORATIF ───────────────────────────────── -->
    <div class="absolute inset-0 pointer-events-none overflow-hidden z-0">
      <div class="absolute -top-32 -right-32 w-96 h-96 rounded-full
                  bg-emerald-500/10 blur-3xl animate-pulse"></div>
      <div class="absolute -bottom-20 -left-20 w-80 h-80 rounded-full
                  bg-blue-400/10 blur-3xl animate-pulse"
           style="animation-delay: 1s;"></div>
    </div>

    <div class="max-w-6xl mx-auto w-full relative z-10">
      <div class="flex flex-col-reverse md:flex-row items-center justify-between gap-12">

        <!-- ── TEXTE GAUCHE ───────────────────────────────── -->
        <div class="flex-1 text-center md:text-left">

          <p class="text-blue-300 font-mono text-lg mb-2 animate-slide-up"
             style="animation-delay: 0.1s;">
            {{ t.hero.greeting }}
          </p>

          <h1 class="text-5xl md:text-7xl font-bold mb-4 leading-none tracking-tight
                     text-white animate-slide-up"
              style="animation-delay: 0.2s;">
            MOUSSAIF<br>
            <span class="text-transparent bg-clip-text
                         bg-gradient-to-r from-emerald-400 to-blue-400">
              SAAD
            </span>
          </h1>

          <h2 class="text-lg md:text-xl text-emerald-400 font-mono mb-6
                     animate-slide-up" style="animation-delay: 0.3s;">
            {{ t.hero.title }}
          </h2>

          <p class="text-blue-200/70 text-base max-w-lg mb-10 leading-relaxed
                    animate-slide-up" style="animation-delay: 0.4s;">
            {{ t.hero.desc }}
          </p>

          <div class="flex gap-4 justify-center md:justify-start flex-wrap
                      animate-slide-up" style="animation-delay: 0.5s;">
            <button @click="scrollTo('projects')"
                    class="group px-8 py-3 rounded-lg font-mono text-sm
                           bg-emerald-500 hover:bg-emerald-400 text-blue-950
                           font-bold transition-all duration-300 hover:-translate-y-1
                           hover:shadow-xl hover:shadow-emerald-500/30
                           flex items-center gap-2">
              {{ t.hero.cta }}
              <span class="transition-transform duration-300 group-hover:translate-x-1">→</span>
            </button>

            <button @click="scrollTo('contact')"
                    class="px-8 py-3 rounded-lg font-mono text-sm
                           border border-blue-500/50 text-blue-200
                           hover:border-emerald-400 hover:text-emerald-400
                           hover:bg-emerald-400/5
                           transition-all duration-300 hover:-translate-y-1">
              {{ t.hero.contact }}
            </button>
          </div>

          <div class="flex gap-10 mt-14 justify-center md:justify-start
                      animate-slide-up" style="animation-delay: 0.6s;">
            <div v-for="stat in stats" :key="stat.label" class="text-center md:text-left">
              <div class="text-3xl font-bold text-emerald-400">{{ stat.value }}</div>
              <div class="text-xs font-mono text-blue-300/60 mt-1">{{ stat.label }}</div>
            </div>
          </div>
        </div>

        <!-- ── PHOTO DROITE ───────────────────────────────── -->
        <div class="flex-shrink-0 flex items-center justify-center animate-fade-in"
             style="animation-delay: 0.3s;">
          <div class="relative">
            <div class="absolute inset-0 rounded-full
                        bg-gradient-to-r from-emerald-400 via-blue-400 to-emerald-400
                        animate-spin-slow opacity-70 scale-105 blur-sm"></div>
            <div class="absolute -inset-3 rounded-full border border-emerald-400/20 animate-spin-reverse"></div>
            <div class="absolute -inset-6 rounded-full border border-dashed border-blue-400/20 animate-spin-slow"
                 style="animation-duration: 15s;"></div>

            <div class="relative w-64 h-64 md:w-80 md:h-80 rounded-full
                        bg-gradient-to-br from-blue-800 to-blue-900
                        border-4 border-blue-700/50 overflow-hidden
                        hover:scale-105 transition-transform duration-500
                        cursor-pointer group z-10">
              <img src="/saadAI.png" alt="MOUSSAIF SAAD"
                   class="w-full h-full object-cover object-center
                          transition-transform duration-500 group-hover:scale-110"
                   @error="photoError = true"
                   v-if="!photoError" />
              <div v-else class="w-full h-full flex flex-col items-center justify-center
                                  bg-gradient-to-br from-blue-800 to-blue-900">
                <span class="text-5xl font-bold text-emerald-400 mb-2">MS</span>
              </div>
              <div class="absolute inset-0 bg-emerald-500/10 opacity-0
                          group-hover:opacity-100 transition-opacity duration-300"></div>
            </div>

            <div class="absolute -bottom-3 left-1/2 -translate-x-1/2
                        bg-blue-900 border border-emerald-500/40
                        px-4 py-1.5 rounded-full flex items-center gap-2 z-20
                        shadow-lg shadow-blue-950/50">
              <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
              <span class="font-mono text-xs text-emerald-400 whitespace-nowrap">
                Full Stack Engineer
              </span>
            </div>

            <div class="absolute -top-3 -right-3 w-5 h-5 rounded-full bg-emerald-400
                        shadow-[0_0_15px_rgba(16,185,129,0.9)] animate-pulse z-20"></div>
            <div class="absolute -bottom-3 -left-3 w-4 h-4 rounded-full bg-blue-400
                        shadow-[0_0_15px_rgba(96,165,250,0.9)] animate-pulse z-20"
                 style="animation-delay: 0.7s;"></div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection',
  props: { t: Object },

  data() {
    return {
      photoError: false,
      stats: [
        { value: '2+',  label: 'Ans / Years' },
        { value: '12',  label: 'Projets / Projects' },
        { value: '99%', label: 'Satisfaction' },
      ],
      // Position curseur principal (suit la souris immédiatement)
      cursor: { x: -100, y: -100, rx: -100, ry: -100 },
      // Pour l'animation douce du ring
      animFrame: null,
    }
  },

  mounted() {
    this.initCanvas()
    this.initCursor()
  },

  beforeUnmount() {
    window.removeEventListener('mousemove', this._onMouseMove)
    if (this.animFrame) cancelAnimationFrame(this.animFrame)
  },

  methods: {
    scrollTo(id) {
      document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
    },

    // ── CURSEUR PERSONNALISÉ ─────────────────────────────
    initCursor() {
      let rx = -100, ry = -100
      const lerp = (a, b, t) => a + (b - a) * t

      this._onMouseMove = (e) => {
        this.cursor.x = e.clientX
        this.cursor.y = e.clientY
      }
      window.addEventListener('mousemove', this._onMouseMove)

      // Ring suit avec délai (interpolation)
      const animate = () => {
        rx = lerp(rx, this.cursor.x, 0.12)
        ry = lerp(ry, this.cursor.y, 0.12)
        this.cursor.rx = rx
        this.cursor.ry = ry
        this.animFrame = requestAnimationFrame(animate)
      }
      animate()
    },

    // ── CANVAS 3D PARTICULES ─────────────────────────────
    initCanvas() {
      const canvas = this.$refs.canvas3d
      if (!canvas) return
      const ctx = canvas.getContext('2d')

      const resize = () => {
        canvas.width  = canvas.offsetWidth
        canvas.height = canvas.offsetHeight
      }
      resize()
      window.addEventListener('resize', resize)

      // Création des particules 3D
      const COUNT = 80
      const particles = Array.from({ length: COUNT }, () => ({
        x:  Math.random() * canvas.width,
        y:  Math.random() * canvas.height,
        z:  Math.random() * 800 + 100,   // profondeur 3D
        vx: (Math.random() - 0.5) * 0.4,
        vy: (Math.random() - 0.5) * 0.4,
        vz: (Math.random() - 0.5) * 1.5, // vitesse en profondeur
        r:  Math.random() * 2 + 0.5,
        // couleur aléatoire entre vert émeraude et bleu
        color: Math.random() > 0.5
          ? `rgba(52, 211, 153,`   // emerald-400
          : `rgba(96, 165, 250,`,  // blue-400
      }))

      const cx = () => canvas.width  / 2
      const cy = () => canvas.height / 2
      const FL = 500  // longueur focale pour projection 3D

      const draw = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height)

        particles.forEach((p, i) => {
          // ── Mise à jour position 3D ──
          p.x += p.vx
          p.y += p.vy
          p.z += p.vz

          // Rebond sur les bords en profondeur
          if (p.z < 50 || p.z > 900) p.vz *= -1
          // Rebond sur les bords X/Y
          if (p.x < 0 || p.x > canvas.width)  p.vx *= -1
          if (p.y < 0 || p.y > canvas.height) p.vy *= -1

          // ── Projection 3D → 2D ──
          const scale = FL / (FL + p.z)
          const sx = (p.x - cx()) * scale + cx()
          const sy = (p.y - cy()) * scale + cy()
          const sr = p.r * scale * 2.5

          // Plus la particule est proche (z petit) → plus opaque
          const alpha = (1 - p.z / 900) * 0.7 + 0.1

          // ── Dessin de la particule ──
          ctx.beginPath()
          ctx.arc(sx, sy, Math.max(sr, 0.3), 0, Math.PI * 2)
          ctx.fillStyle = `${p.color}${alpha})`
          ctx.fill()

          // ── Connexion entre particules proches ──
          particles.slice(i + 1, i + 5).forEach(p2 => {
            const scale2 = FL / (FL + p2.z)
            const sx2 = (p2.x - cx()) * scale2 + cx()
            const sy2 = (p2.y - cy()) * scale2 + cy()

            const dist = Math.hypot(sx - sx2, sy - sy2)
            if (dist < 120) {
              const lineAlpha = (1 - dist / 120) * 0.15
              ctx.beginPath()
              ctx.moveTo(sx, sy)
              ctx.lineTo(sx2, sy2)
              ctx.strokeStyle = `rgba(96, 165, 250, ${lineAlpha})`
              ctx.lineWidth = 0.5
              ctx.stroke()
            }
          })
        })

        requestAnimationFrame(draw)
      }
      draw()
    },
  },
}
</script>

<style scoped>
/* ── Curseur dot (suit immédiatement) ── */
.cursor-dot {
  position: fixed;
  width: 8px;
  height: 8px;
  background: #34d399;
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  z-index: 9999;
  transition: width 0.2s, height 0.2s, background 0.2s;
  box-shadow: 0 0 10px rgba(52, 211, 153, 0.8);
}

/* ── Curseur ring (suit avec délai) ── */
.cursor-ring {
  position: fixed;
  width: 36px;
  height: 36px;
  border: 1.5px solid rgba(52, 211, 153, 0.6);
  border-radius: 50%;
  pointer-events: none;
  transform: translate(-50%, -50%);
  z-index: 9998;
  transition: width 0.3s, height 0.3s;
}

/* ── Animations ── */
@keyframes fade-in {
  from { opacity: 0; }
  to   { opacity: 1; }
}
.animate-fade-in { animation: fade-in 0.8s ease both; }

@keyframes slide-up {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
.animate-slide-up { animation: slide-up 0.7s ease both; }

@keyframes spin-slow {
  from { transform: rotate(0deg) scale(1.05); }
  to   { transform: rotate(360deg) scale(1.05); }
}
.animate-spin-slow { animation: spin-slow 8s linear infinite; }

@keyframes spin-reverse {
  from { transform: rotate(360deg); }
  to   { transform: rotate(0deg); }
}
.animate-spin-reverse { animation: spin-reverse 12s linear infinite; }
</style>