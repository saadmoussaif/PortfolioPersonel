<template>
  <!-- Section À propos -->
  <section id="about" class="py-24 px-6 bg-gray-50 dark:bg-gray-900">
    <div class="max-w-5xl mx-auto">

      <!-- Label + Titre -->
      <div class="mb-14">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                  uppercase tracking-widest mb-3">
          // {{ t.about.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold">{{ t.about.title }}</h2>
      </div>

      <div class="grid md:grid-cols-2 gap-12 items-center">

        <!-- Texte de présentation -->
        <div>
          <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed mb-8">
            {{ t.about.desc }}
          </p>

          <!-- Statistiques -->
          <div class="grid grid-cols-3 gap-6">
            <div v-for="stat in stats" :key="stat.label"
                 class="bg-white dark:bg-gray-800 rounded-xl p-4
                        border border-gray-200 dark:border-gray-700 text-center">
              <div class="text-2xl font-bold text-emerald-600 dark:text-emerald-400">
                {{ stat.value }}
              </div>
              <div class="text-xs font-mono text-gray-500 mt-1">
                {{ stat.label }}
              </div>
            </div>
          </div>
        </div>

        <!-- Carte profil -->
        <div class="bg-white dark:bg-gray-800 rounded-2xl p-8
                    border border-gray-200 dark:border-gray-700">
          
          <!-- Avatar initiales -->
          <div class="w-20 h-20 rounded-full bg-emerald-100 dark:bg-emerald-900/30
                      flex items-center justify-center
                      text-emerald-600 dark:text-emerald-400
                      text-2xl font-bold mb-6">
            AM
          </div>

          <!-- Infos -->
          <div class="space-y-3">
            <div v-for="info in infos" :key="info.label"
                 class="flex justify-between text-sm
                        border-b border-gray-100 dark:border-gray-700 pb-2">
              <span class="font-mono text-gray-400">{{ info.label }}</span>
              <span class="text-gray-700 dark:text-gray-300">{{ info.value }}</span>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'AboutSection',

  props: {
    t: Object,
  },

  data() {
    return {
      stats: [
        { value: '4+', label: 'Ans / Years' },
        { value: '12', label: 'Projets' },
        { value: '99%', label: 'Clients' },
      ],
      infos: [
        { label: 'Nom / Name', value: 'MOUSSAIF SAAD' },
        { label: 'Role', value: 'Full Stack Engineer' },
        { label: 'Location', value: 'Casablanca,Maroc' },
        { label: 'Email', value: 'moussaifsaad4@gmail.com' },
        { label: 'Status', value: '✅ Disponible' },
      ],
    }
  },
}
</script>