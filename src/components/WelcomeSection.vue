<script setup>
import faceicon from '../assets/facegen.png'

defineProps(['items'])


</script>

<template>
  <div id="welcome" class="flex items-center  justify-center h-screen bg-blue-900 border border-white">
    <div class="ml-16 flex flex-col justify-center w-3/4 h-3/4 text-white">
      <div class="flex ">
          <img :src="faceicon" class="h-72 transition-transform duration-300 hover:scale-x-[-1]" alt="" >
          <div class="relative flex flex-col justify-center items-center w-dvh">
            <p class="text-lg mt-2 absolute top-0 left-0">Hello, I'm <span class="text-cyan-400">Syahrul...</span></p>
            <h1 class="text-4xl font-bold">"Life like a <span class="text-cyan-400 ">Game</span>. I can <span class="text-green-500">Win</span> and i can <span class="text-red-500">Lose</span>. But how about draw? Haha, i don't know!"</h1>
          </div>
      </div>
      <div class="">
          <p class="text-blue-100">I'am a Student and Developer</p>
          <p class="text-xl text-gray-200 leading-relaxed">
              Welcome to my personal portfolio. Here, I will introduce who I am, my skills, and some of the projects I have worked on. Feel free to explore this page to get to know me better. Want to connect? Let's contat me!
          </p>
      </div>
    </div>

    
  </div>
</template>

<style scoped>

</style>