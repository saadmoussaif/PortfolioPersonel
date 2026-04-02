<template>
  <!-- Section Projets -->
  <section id="projects" class="py-24 px-6 bg-gray-50 dark:bg-gray-900">
    <div class="max-w-5xl mx-auto">

      <!-- Label + Titre -->
      <div class="mb-14">
        <p class="font-mono text-xs text-emerald-600 dark:text-emerald-400 
                  uppercase tracking-widest mb-3">
          // {{ t.projects.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold">{{ t.projects.title }}</h2>
      </div>

      <!-- Grille de projets -->
      <div class="grid md:grid-cols-2 gap-6">
        <div v-for="(proj, i) in projects" :key="proj.title"
             class="bg-white dark:bg-gray-800 rounded-xl p-6
                    border border-gray-200 dark:border-gray-700
                    hover:border-emerald-500 hover:-translate-y-1
                    transition-all duration-300 cursor-pointer group">

          <!-- Numéro + flèche -->
          <div class="flex justify-between items-center mb-4">
            <span class="font-mono text-xs text-gray-400">
              {{ String(i+1).padStart(2,'0') }}
            </span>
            <span class="text-gray-300 dark:text-gray-600 
                         group-hover:text-emerald-500 
                         group-hover:-translate-y-0.5 group-hover:translate-x-0.5
                         transition-all text-xl">↗</span>
          </div>

          <!-- Titre -->
          <h3 class="text-xl font-bold mb-3">{{ proj.title }}</h3>

          <!-- Description -->
          <p class="text-gray-500 dark:text-gray-400 text-sm leading-relaxed mb-4">
            {{ proj.desc }}
          </p>

          <!-- Tags technologies -->
          <div class="flex flex-wrap gap-2 mb-4">
            <span v-for="tag in proj.tags" :key="tag"
                  class="px-2 py-1 text-xs font-mono rounded
                         bg-yellow-50 dark:bg-yellow-900/20
                         border border-yellow-200 dark:border-yellow-800
                         text-yellow-700 dark:text-yellow-400">
              {{ tag }}
            </span>
          </div>

          <!-- Métriques -->
          <div class="flex gap-3 flex-wrap">
            <span v-for="m in proj.metrics" :key="m"
                  class="text-xs font-mono text-emerald-600 dark:text-emerald-400
                         border border-emerald-200 dark:border-emerald-800
                         px-2 py-1 rounded">
              {{ m }}
            </span>
          </div>

        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProjectsSection',

  props: {
    t: Object,
  },

  data() {
    return {
      projects: [
        {
          title: 'SaaS Analytics Dashboard',
          desc: 'Tableau de bord temps réel pour une startup fintech. 50 000 utilisateurs actifs.',
          tags: ['Vue.js', 'Node.js', 'WebSocket', 'PostgreSQL'],
          metrics: ['50k users', '< 200ms', '99.9% uptime'],
        },
        {
          title: 'API Microservices Platform',
          desc: 'Architecture distribuée pour une plateforme e-commerce sur AWS.',
          tags: ['Python', 'Docker', 'Kubernetes', 'Redis'],
          metrics: ['12 services', 'AWS EKS', 'Auto-scaling'],
        },
        {
          title: 'Mobile App React Native',
          desc: 'Application cross-platform iOS/Android avec synchronisation offline.',
          tags: ['React Native', 'TypeScript', 'GraphQL'],
          metrics: ['10k+ DL', '4.8 ★', 'iOS & Android'],
        },
        {
          title: 'DevOps Automation Tools',
          desc: 'Suite d\'outils CLI pour automatiser les déploiements et monitorer l\'infrastructure.',
          tags: ['Python', 'Bash', 'Terraform', 'Prometheus'],
          metrics: ['-60% deploy time', 'Open source'],
        },
      ],
    }
  },
}
</script>