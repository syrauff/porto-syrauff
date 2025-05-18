<script setup>
import photo from '../assets/foto.png'

</script>

<template>
<div id="about" class="flex items-center justify-center h-screen bg-sky-950 text-white">
  <div class="ml-16 flex flex-col  w-3/4 h-3/4 border p-4 border-red-300">
  <div class="flex justify-center items-center">
    <h2 class="text-3xl font-bold text-cyan-400">About me</h2>
  </div>
    <!-- Foto / Ilustrasi -->
    <div class="flex">
    <div class="">
      <img :src="photo" alt="My Photo" class="w-60 m-4 object-cover hover:scale-105 transition duration-300">
    </div>
    <!-- Konten About -->
    <div class="flex flex-col px-10 gap-3">
      
      <p class="text-gray-300 leading-relaxed text-xl">
        I'm <span class="text-cyan-300 font-semibold">Syahrul Ridho R. Rauf</span>, an enthusiastic developer who loves building creative and useful tech products. Currently, I'm focusing on web development, machine learning, and mapping technologies.
      </p>
      <p class="text-blue-100 text-sm">
        <svg class="inline mb-1 w-6 h-6 text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18Zm0 0a8.949 8.949 0 0 0 4.951-1.488A3.987 3.987 0 0 0 13 16h-2a3.987 3.987 0 0 0-3.951 3.512A8.948 8.948 0 0 0 12 21Zm3-11a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"/>
        </svg>
        Now, I am <span class="text-sky-400">Student • Developer • Explorer • Gamer</span>
      </p>
      
      <p class="text-blue-100 text-sm">
        <svg class="inline mb-1 w-6 h-6text-white" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 13a3 3 0 1 0 0-6 3 3 0 0 0 0 6Z"/>
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.8 13.938h-.011a7 7 0 1 0-11.464.144h-.016l.14.171c.1.127.2.251.3.371L12 21l5.13-6.248c.194-.209.374-.429.54-.659l.13-.155Z"/>
        </svg>

        I live in <span class="text-purple-200">Kota Gorontalo, Gorontalo, Indonesia</span>
        </p>
    </div>
  </div>
  <div class="flex mt-15">
    <div class="flex px-5 flex-col w-1/2">
      <h2 class="text-3xl font-bold text-cyan-400 text-center mb-3 border-b">
        <svg class="inline w-9 h-9 mb-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 20v-9l-4 1.125V20h4Zm0 0h8m-8 0V6.66667M16 20v-9l4 1.125V20h-4Zm0 0V6.66667M18 8l-6-4-6 4m5 1h2m-2 3h2"/>
        </svg>
        Education
      </h2>
      <p class="text-blue-100">
        Saya telah menyelesaikan pendidikan saya di
      </p>
      <ul class="list-inside text-blue-100 invisible">
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">SD Muhammadiyah Kota Utara</li>
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">MTs. Negeri 1 Kota Gorontalo</li>
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">MAN Insan Cendekia Gorontalo</li>
      </ul>
      <p class="text-blue-100 mt-3">dan sekarang saya sedang menempiuh studi di</p>
      <ul class="list-inside text-blue-100">
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">Universitas Negeri Gorontalo</li>
      </ul>
    </div>
    <div class="flex px-5 flex-col w-1/2">
      <h2 class="text-3xl font-bold text-cyan-400 text-center mb-3 border-b">
        <svg class="inline w-9 h-9 mb-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5.35709 16V5.78571c0-.43393.34822-.78571.77777-.78571H18.5793c.4296 0 .7778.35178.7778.78571V16M5.35709 16h-1c-.55229 0-1 .4477-1 1v1c0 .5523.44771 1 1 1H20.3571c.5523 0 1-.4477 1-1v-1c0-.5523-.4477-1-1-1h-1M5.35709 16H19.3571M9.35709 8l2.62501 2.5L9.35709 13m4.00001 0h2"/>
        </svg>
        Experience
      </h2>
      <p class="text-blue-100">Saya berpengalaman dalam pembuatan:</p>
      <ul class="list-inside text-blue-100">
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">Diagram Flow Data</li>
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">Website</li>
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">Model Machine Learning</li>
        <li class="before:content-['→'] before:mr-2 before:text-blue-300">Document</li>
      </ul>
    </div>
  </div>
  </div>
</div>
</template>

<style scoped>

</style>