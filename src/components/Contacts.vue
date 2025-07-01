<template>
  <section ref="contact" class="bg-neutral-950 text-white w-full py-20 px-6 flex flex-col items-center gap-20 min-h-screen">
    <h2 class="text-4xl md:text-6xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-violet-500 to-fuchsia-500 drop-shadow-lg">
      Contacto
    </h2>

    <div class="flex items-center gap-6 mt-10">
      <div v-for="(img, index) in socialMedia" :key="index" class="border rounded-2xl p-2">
        <a :href="img.link" target="_black"><img :src="img.img_src" alt="" class="w-10"></a>
      </div>
    </div>

  </section>
</template>


<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { eventBus } from '../utils/eventBus.js'

const socialMedia = ref([
  {title: 'Instagram', img_src: '/instagram.svg', link: 'https://x.com/ololumas'},
  {title: 'Github', img_src: '/github.svg', link: 'https://github.com/EliseuFranco'},
  {title: 'email', img_src: '/email.svg', link:'mailto:eliseufranco26@hotmail.com'}

])

</script>
