<script setup>
import faceicon from '../assets/facegen.png'

defineProps(['items'])


</script>

<template>
  <div id="welcome" class="min-h-screen flex items-center bg-blue-900">
    <div class="ml-16 flex flex-col  justify-center text-white border">
    <div class="flex h-full mx-auto items-stretch border">
        <img :src="faceicon" class="h-72 transition-transform duration-300 hover:scale-x-[-1]" alt="" >
        <div class="relative flex flex-col justify-center items-center w-dvh">
          <p class="text-lg mt-2 absolute top-0 left-0">Hello, I'm <span class="text-cyan-400">Syahrul...</span></p>
          <h1 class="text-4xl font-bold">"Life like a <span class="text-cyan-400 ">Game</span>. I can <span class="text-green-500">Win</span> and i can <span class="text-red-500">Lose</span>. But how about draw? Haha, i don't know!"</h1>
        </div>
    </div>
    <div class="h-full mx-auto w-9/12 items-stretch">
        <p class="text-blue-100">I'am a Student and Developer</p>
        <p class="text-xl text-gray-200 leading-relaxed">
            Welcome to my personal portfolio. Here, I will introduce who I am, my skills, and some of the projects I have worked on. Feel free to explore this page to get to know me better. Want to connect? Let's contat me!
        </p>
    </div>
      
    </div>
    <div class="flex flex-col justify-center items-center w-20">
      <svg class="w-6 h-6 text-cyan-200 hover:mb-3 hover:w-8 hover:h-8 hover:animate-bounce " aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
      <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7 7.674 1.3a.91.91 0 0 0-1.348 0L1 7"/>
      </svg>
      <svg class="w-8 h-8 text-cyan-200" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
        <path stroke="currentColor" stroke-linecap="round" stroke-width="2" d="M6 12h.01m6 0h.01m5.99 0h.01"/>
      </svg>

      <svg class="w-6 h-6 text-cyan-200 hover:mt-3 hover:w-8 hover:h-8 hover:animate-bounce " aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 5.326 5.7a.909.909 0 0 0 1.348 0L13 1"/>
      </svg>
    </div>
  </div>
</template>

<style scoped>

</style>