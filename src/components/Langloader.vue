<template>
  <!-- Overlay de chargement lors du changement de langue -->
  <Transition name="loader">
    <div v-if="show"
         class="fixed inset-0 z-[9999] flex flex-col items-center justify-center
                bg-blue-950/95 backdrop-blur-md">

      <!-- Cercles animés -->
      <div class="relative w-24 h-24 mb-8">
        <!-- Cercle extérieur -->
        <div class="absolute inset-0 rounded-full border-2 border-emerald-400/20
                    animate-spin-slow"></div>
        <!-- Cercle milieu -->
        <div class="absolute inset-2 rounded-full border-2 border-t-emerald-400 border-r-transparent
                    border-b-transparent border-l-transparent animate-spin"
             style="animation-duration: 0.8s;"></div>
        <!-- Cercle intérieur -->
        <div class="absolute inset-4 rounded-full border-2 border-b-blue-400 border-t-transparent
                    border-r-transparent border-l-transparent animate-spin"
             style="animation-duration: 1.2s; animation-direction: reverse;"></div>
        <!-- Point central -->
        <div class="absolute inset-0 flex items-center justify-center">
          <div class="w-3 h-3 rounded-full bg-emerald-400 animate-pulse
                      shadow-[0_0_12px_rgba(52,211,153,0.8)]"></div>
        </div>
      </div>

      <!-- Drapeaux qui s'échangent -->
      <div class="flex items-center gap-4 mb-6">
        <div class="text-3xl transition-all duration-500"
             :class="from === 'fr' ? 'opacity-100 scale-100' : 'opacity-40 scale-75'">
          🇫🇷
        </div>
        <!-- Flèche animée -->
        <div class="text-emerald-400 font-mono text-xl animate-bounce">→</div>
        <div class="text-3xl transition-all duration-500"
             :class="from === 'en' ? 'opacity-100 scale-100' : 'opacity-40 scale-75'">
          🇬🇧
        </div>
      </div>

      <!-- Texte de chargement -->
      <p class="font-mono text-sm text-emerald-400 animate-pulse">
        {{ from === 'fr' ? 'Switching to English...' : 'Passage en Français...' }}
      </p>

      <!-- Barre de progression -->
      <div class="mt-6 w-48 h-0.5 bg-blue-800 rounded-full overflow-hidden">
        <div class="h-full bg-gradient-to-r from-emerald-400 to-blue-400 rounded-full
                    animate-progress"></div>
      </div>

    </div>
  </Transition>
</template>

<script>
export default {
  name: 'LangLoader',

  props: {
    // true = afficher le loader
    show: Boolean,
    // langue actuelle avant le changement ('fr' ou 'en')
    from: String,
  },
}
</script>

<style scoped>
/* Animation d'entrée/sortie du loader */
.loader-enter-active { transition: opacity 0.2s ease; }
.loader-leave-active { transition: opacity 0.4s ease; }
.loader-enter-from  { opacity: 0; }
.loader-leave-to    { opacity: 0; }

/* Barre de progression qui se remplit */
@keyframes progress {
  from { width: 0%; }
  to   { width: 100%; }
}
.animate-progress {
  animation: progress 0.6s ease-in-out forwards;
}

/* Rotation lente */
@keyframes spin-slow {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
.animate-spin-slow {
  animation: spin-slow 3s linear infinite;
}
</style>