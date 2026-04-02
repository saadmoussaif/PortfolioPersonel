<template>
  <section id="skills"
           class="py-24 px-6 bg-gradient-to-b from-blue-900 to-blue-950 relative overflow-hidden">

    <!-- Fond décoratif -->
    <div class="absolute inset-0 pointer-events-none">
      <div class="absolute top-10 left-1/2 w-96 h-96 rounded-full
                  bg-emerald-500/5 blur-3xl -translate-x-1/2"></div>
      <div class="absolute bottom-0 right-0 w-64 h-64 rounded-full
                  bg-blue-400/5 blur-3xl"></div>
    </div>

    <div class="max-w-6xl mx-auto relative z-10">

      <!-- TITRE -->
      <div class="mb-16 text-center">
        <p class="font-mono text-xs text-emerald-400 uppercase tracking-widest mb-3">
          // {{ t.skills.label }}
        </p>
        <h2 class="text-4xl md:text-5xl font-bold text-white">
          {{ t.skills.title }}
        </h2>
        <div class="mt-4 flex justify-center">
          <div class="h-0.5 w-16 bg-gradient-to-r from-emerald-400 to-blue-400 rounded-full"></div>
        </div>
      </div>

      <!-- CATÉGORIES -->
      <div class="space-y-16">

        <div v-for="(cat, catIndex) in categories"
             :key="cat.name"
             :ref="el => { if(el) catRefs[catIndex] = el }"
             class="transition-all duration-700 ease-out"
             :style="{
               opacity: visibleCats[catIndex] ? 1 : 0,
               transform: visibleCats[catIndex]
                 ? 'translateX(0px)'
                 : catIndex % 2 === 0 ? 'translateX(-60px)' : 'translateX(60px)',
             }">

          <!-- Header catégorie -->
          <div class="flex items-center gap-4 mb-8">
            <div class="w-12 h-12 rounded-xl bg-blue-800 border border-blue-600
                        flex items-center justify-center text-2xl">
              {{ cat.icon }}
            </div>
            <div>
              <h3 class="text-2xl font-bold text-white">{{ cat.name }}</h3>
              <p class="text-xs font-mono text-blue-400">{{ cat.desc }}</p>
            </div>
            <div class="flex-1 h-px bg-gradient-to-r from-blue-700/80 to-transparent ml-4"></div>
          </div>

          <!-- Skills -->
          <div class="grid grid-cols-3 sm:grid-cols-4 md:grid-cols-5 lg:grid-cols-8 gap-4">

            <div v-for="(skill, skillIndex) in cat.skills"
                 :key="skill.name"
                 class="group flex flex-col items-center gap-3"
                 :style="{
                   opacity: visibleCats[catIndex] ? 1 : 0,
                   transform: visibleCats[catIndex] ? 'translateY(0)' : 'translateY(40px)',
                   transition: `opacity 0.5s ease, transform 0.5s ease`,
                   transitionDelay: `${skillIndex * 60}ms`
                 }">

              <div class="w-16 h-16 rounded-2xl
                          bg-blue-800/70 border border-blue-700
                          flex items-center justify-center
                          group-hover:border-emerald-400
                          transition-all duration-300">

                <img :src="skill.logo"
                     class="w-9 h-9 object-contain"
                     :class="skill.invert ? 'brightness-0 invert opacity-80' : ''"
                     @error="(e) => { e.target.style.display='none'; e.target.nextElementSibling.style.display='flex' }" />

                <span class="hidden text-2xl">
                  {{ skill.emoji }}
                </span>

              </div>

              <span class="text-xs font-mono text-blue-400 text-center">
                {{ skill.name }}
              </span>

            </div>

          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'SkillsSection',
  props: { t: Object },

  data() {
    return {
      visibleCats: [false, false, false],
      catRefs: [],

      categories: [
        {
          name: 'Backend',
          icon: '⚙️',
          desc: 'Serveurs · APIs · Bases de données',
          skills: [
              { name: 'Spring Boot', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg', emoji: '🌱' },
            { name: 'Node.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg', emoji: '🟢' },
            { name: 'Python', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg', emoji: '🐍' },
            { name: 'Django', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/django/django-plain.svg', emoji: '🎯', invert: true },
            { name: 'Express', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/express/express-original.svg', emoji: '🚀', invert: true },
          ]
        },
        {
          name: 'Frontend',
          icon: '🎨',
          desc: 'UI · UX',
          skills: [
            { 
  name: 'Angular', 
  logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/angularjs/angularjs-original.svg', 
  emoji: '🅰️' 
},
            { name: 'Vue.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg', emoji: '💚' },
            { name: 'React', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg', emoji: '⚛️' },
            { name: 'JavaScript', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg', emoji: '🟡' },
            {name: 'Tailwind', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/tailwindcss/tailwindcss-original.svg', emoji: '💨' },
          ]
        },
        {
          name: 'DevOps',
          icon: '☁️',
          desc: 'Cloud · CI/CD',
          skills: [
            { name: 'Docker', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg', emoji: '🐳' },
            { name: 'Linux', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linux/linux-original.svg', emoji: '🐧' },
            { name: 'Git', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg', emoji: '🌿' },
            { name: 'Nginx', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nginx/nginx-original.svg', emoji: '🔀' },
            { name: 'Kubernetes', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain.svg', emoji: '⎈' }, { name: 'AWS', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg', emoji: '☁️' },
          ]
        }
      ]
    }
  },

  mounted() {
    this.$nextTick(() => {
      this.catRefs.forEach((el, index) => {
        if (!el) return

        const observer = new IntersectionObserver(
          (entries) => {
            const entry = entries[0]

            if (entry.isIntersecting) {
              this.visibleCats[index] = true
            } else {
              this.visibleCats[index] = false
            }

            this.visibleCats = [...this.visibleCats]
          },
          { threshold: 0.3 }
        )

        observer.observe(el)
      })
    })
  }
}
</script>

<style scoped>
@keyframes float {
  from { transform: translateY(0px); }
  to { transform: translateY(-8px); }
}
</style>