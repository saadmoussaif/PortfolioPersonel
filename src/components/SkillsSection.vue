<template>
  <section id="skills" class="py-24 px-6 bg-white dark:bg-gray-950">
    <div class="max-w-5xl mx-auto">

      <!-- Header -->
      <div class="mb-14">
        <p class="font-mono text-xs text-emerald-600 uppercase tracking-widest mb-3">
          // {{ t.skills.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold">{{ t.skills.title }}</h2>
      </div>

      <!-- Categories -->
      <div class="grid md:grid-cols-3 gap-6 mb-12">
        <div v-for="cat in categories" :key="cat.name"
             class="group bg-gray-50 dark:bg-gray-900 rounded-xl p-6
                    border border-gray-200 dark:border-gray-800
                    hover:border-emerald-500 transition-all duration-300
                    hover:shadow-xl hover:-translate-y-2">

          <h3 class="font-bold text-lg mb-6 flex items-center gap-2">
            <span class="text-emerald-500 text-xl">{{ cat.icon }}</span>
            {{ cat.name }}
          </h3>

          <!-- Skills -->
          <div class="flex flex-wrap gap-4">
            <div v-for="skill in cat.skills" :key="skill.name"
                 class="flex items-center gap-2 px-3 py-2 rounded-lg
                        bg-gray-100 dark:bg-gray-800
                        border border-gray-200 dark:border-gray-700
                        transition-all duration-500
                        group-hover:translate-y-[-8px]
                        group-hover:rotate-1
                        group-hover:scale-110
                        hover:scale-125 hover:-translate-y-2
                        cursor-pointer">

              <!-- LOGO -->
              <img :src="skill.icon" class="w-5 h-5 object-contain" />

              <span class="text-sm font-mono">
                {{ skill.name }}
              </span>

            </div>
          </div>
        </div>
      </div>

      <!-- Tech chips -->
      <div class="flex flex-wrap gap-3">
        <span v-for="tech in techs" :key="tech"
              class="px-4 py-2 font-mono text-xs rounded-lg
                     bg-emerald-50 border border-emerald-200
                     text-emerald-600
                     hover:scale-110 transition-all duration-300">
          {{ tech }}
        </span>
      </div>

    </div>
  </section>
</template>

<script>
export default {
  name: 'SkillsSection',

  props: {
    t: Object,
  },

  data() {
    return {
      categories: [
        {
          name: 'Frontend',
          icon: '◈',
          skills: [
            { name: 'Vue.js', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg' },
            { name: 'React', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg' },
            { name: 'TypeScript', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg' },
            { name: 'Tailwind', icon: 'https://www.vectorlogo.zone/logos/tailwindcss/tailwindcss-icon.svg' },
          ],
        },
        {
          name: 'Backend',
          icon: '◉',
          skills: [
            { name: 'Node.js', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg' },
            { name: 'Python', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg' },
            { name: 'GraphQL', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/graphql/graphql-plain.svg' },
          ],
        },
        {
          name: 'DevOps',
          icon: '◎',
          skills: [
            { name: 'Docker', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg' },
            { name: 'Kubernetes', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain.svg' },
            { name: 'AWS', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg' },
          ],
        },
      ],

      techs: [
        'PostgreSQL', 'MongoDB', 'Redis', 'Next.js',
        'Express', 'FastAPI', 'GitHub Actions',
        'Linux', 'Jest', 'Figma', 'Nginx',
      ],
    }
  },
}
</script>