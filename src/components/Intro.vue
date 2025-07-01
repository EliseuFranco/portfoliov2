<template>
  <section class="flex justify-center flex-col gap-3 items-center bg-neutral-950 min-h-screen text-white" id="about">
    <h5 class="font-bold text-2xl">Fullstack developer <span class="text-fuchsia-500">&lt;/&gt;</span></h5>
      <div class="flex flex-col flex-start justify-center items-center gap-3">
        <img :src="myImg" alt="" class="w-32 h-32 rounded-full object-cover">
        <p><strong class="text-xl text-transparent bg-clip-text bg-gradient-to-r from-violet-500 to-fuchsia-500 md:text-6xl">{{ fullName }}</strong> Portfolio</p>
        <span class="text-xs">Scroll to know more about-me</span>

        <div class="flex items-center">
          <button class="flex items-center cursor-pointer" @click="scrollToAbout">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-8  rounded-full p-1 text-fuchsia-600 font-bold animate-bounce duration-1000 ">
              <path fill-rule="evenodd" d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm-.53 14.03a.75.75 0 0 0 1.06 0l3-3a.75.75 0 1 0-1.06-1.06l-1.72 1.72V8.25a.75.75 0 0 0-1.5 0v5.69l-1.72-1.72a.75.75 0 0 0-1.06 1.06l3 3Z" clip-rule="evenodd" />
            </svg>
          </button>
        </div>
      </div>

      <div class="flex items-center mt-30 gap-3  w-full overflow-hidden">
        <div class="flex items-center justify-end gap-9 carroussel w-full overflow-hidden ">
          <img v-for="item in imgObject" :key="item.id" :src="item.src" class="w-10">
        </div>
      </div>
      
  </section>
  
</template>


<script setup>
    import { ref, onMounted } from 'vue'
    import About from './About.vue'

    import { eventBus } from '../utils/eventBus.js'
   

    const scrollToAbout = () => {
      eventBus.emit('scroll-to-about')
    }

    const myImg = ref('/me.jpeg')
    const fullName = ref('')
  

    const imgObject = ref([
      {id: 1, src: '/vue.svg'},
      {id: 2, src: '/javascript.svg'},
      {id: 3, src: '/python.svg'},
      {id: 4, src: '/html.svg'},
      {id: 5, src: '/css.svg'},
      {id: 6, src: '/flask.svg'},
      {id: 7, src: '/tailwind.svg'},
    ])

    const nome = ref("Eliseu Franco Samulolo's")
    let cont = 0;


    const count = ref(0)
    const displayGreeting = () => {
       fullName.value = 'Good morning'
    }

    onMounted(() => {
      const typingInterval = setInterval(() =>{

        if (cont < nome.value.length) {
         fullName.value += nome.value[cont]
          cont++
        }
        else {
          clearInterval(typingInterval)
        }
      }, 200)
      
    })
</script>


<style scoped>


  .carroussel {
    animation: scroll 20s linear infinite;
  }

  @keyframes scroll {
    0% {
      transform: translateX(20%);
      
    }
    100% {
      transform: translateX(-100%);
    }
  }


  

</style>
