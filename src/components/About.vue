<template>

    <section  ref="about" class="relative flex gap-6 p-10 justify-center items-center flex-col bg-black w-full min-h-96 ">
        <h1 class="text-4xl md:text-9xl font-bold text-transparent bg-gradient-to-r from-violet-500 to-fuchsia-500 bg-clip-text">
             About me
        </h1>
         <div class="flex gap-5 w-full max-w-2xl transition-opacity duration-1000 ease-in-out"
         :class="visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-10'">
      
      <div class="flex flex-col gap-5 p-5 justify-center">

        <p class="text-gray-300 text-justify">
          Formado em Gestão e Informática com foco em desenvolvimento web.
          Experiência com <span class="text-fuchsia-400 font-semibold">HTML, CSS, JavaScript, Vue.js, Flask</span> e
          base de dados <span class="text-violet-400 font-semibold">PostgreSQL</span>.
          Comprometido com <span class="text-fuchsia-400 font-semibold">aprendizado contínuo</span> e entrega de soluções eficazes.
        </p>

        <div class="flex items-center gap-5 mb-30">
          <a :href="cv" download
             class=" flex items-center gap-1 bg-gradient-to-r from-violet-500 to-fuchsia-500 hover:opacity-80 text-white border p-2 rounded-2xl">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-6">
            <path fill-rule="evenodd" d="M12 2.25a.75.75 0 0 1 .75.75v11.69l3.22-3.22a.75.75 0 1 1 1.06 1.06l-4.5 4.5a.75.75 0 0 1-1.06 0l-4.5-4.5a.75.75 0 1 1 1.06-1.06l3.22 3.22V3a.75.75 0 0 1 .75-.75Zm-9 13.5a.75.75 0 0 1 .75.75v2.25a1.5 1.5 0 0 0 1.5 1.5h13.5a1.5 1.5 0 0 0 1.5-1.5V16.5a.75.75 0 0 1 1.5 0v2.25a3 3 0 0 1-3 3H5.25a3 3 0 0 1-3-3V16.5a.75.75 0 0 1 .75-.75Z" clip-rule="evenodd" />
            </svg>

                Download CV
          </a>
          <button class="text-fuchsia-400 cursor-pointer hover:underline" @click="scrollToProjects">Ver projetos</button>
      </div>
      </div>
    </div>
    </section>

</template>


<script setup>

import { onMounted, ref , onBeforeUnmount} from "vue";
 import { eventBus } from '../utils/eventBus.js'

    const about = ref(null)
    const visible = ref(false)
    const cv = ref('/cv.pdf')

    let observer;


    const scrollToAbout = () => {
        about.value?.scrollIntoView({ behavior: 'smooth' })
    }

    const scrollToProjects = () => {
        eventBus.emit('scroll-to-projects')
    }

    onMounted(() => {
        observer = new IntersectionObserver(([entry]) => {
            visible.value = entry.isIntersecting

        }, {threshold: 0.6})

        if(about.value) observer.observe(about.value)
        
        eventBus.on('scroll-to-about', scrollToAbout)
    })

     onBeforeUnmount(() => {
        if (about.value && observer) observer.unobserve(about.value)
        })




</script>

<style scoped>


</style>