<template>
  <section ref="projects" class="bg-neutral-950 py-20 px-6 w-full min-h-screen text-white flex flex-col items-center justify-center gap-10">
    
    <h2 class="text-4xl md:text-6xl font-extrabold text-transparent bg-gradient-to-r from-violet-500 to-fuchsia-500 bg-clip-text p-3">
      Projetos 
    </h2>

    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 max-w-7xl w-full transition-all duration-1000">

      <div v-for="project in projectList" :key="project.id"
           class="rounded-2xl p-5 shadow-lg border transform transition-all duration-700 hover:scale-[1.02] shadow hover:shadow-gray-800" :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'">
        <img :src="project.image" alt="project preview" class=" mb-4 h-40 w-full object-contain  p-5"/>
        <h3 class="text-xl font-semibold text-fuchsia-400">{{ project.title }}</h3>
        <p class="text-sm text-gray-300 mt-2">{{ project.description }}</p>
        <a :href="project.link" target="_blank" class="inline-block mt-4 text-sm text-violet-400 hover:underline">
          Ver Projeto →
        </a>
      </div>
    </div>
  </section>
</template>


<script setup>

    import {onMounted, onBeforeUnmount, ref} from 'vue'
    import { eventBus } from '../utils/eventBus.js'
    import { projectList } from '../utils/db.js'

    const projects = ref('')
    const visible = ref(false)
    let observer;

    const scrollToProjects = () => {
        projects.value?.scrollIntoView({behavior: 'smooth'})
    }

    onMounted(() => {
        observer = new IntersectionObserver(([entry])=>{
            visible.value = entry.isIntersecting
        }, {threshold: 0.2, rootMargin: '0px 0px -100px 0px'})

        if(projects.value && observer) observer.observe(projects.value)

        eventBus.on('scroll-to-projects', scrollToProjects)
        
    })

    onBeforeUnmount(() => {
        if(observer && projects.value) observer.unobserve(projects.value)
    })

</script>



<style scoped>

    .fade-up{
        animation: app 3s alternate;
    }

    @keyframes app {
        100%{
            transform: translateY(0);
        }
        0%{
            transform: translateY(100%);
        }
    }

</style>