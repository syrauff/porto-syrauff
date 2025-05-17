<script setup>
import photo from '../assets/foto.png'

</script>

<template>
<div id="about" class="bg-sky-950 h-screen flex flex-col justify-center text-white py-16 lg:px-16 ">
  <div class="ml-16 flex flex-col lg:flex-row items-center border border-b-cyan-300">
    <!-- Foto / Ilustrasi -->
    <div class="">
      <img :src="photo" alt="My Photo" class="w-60 object-cover shadow-lg hover:scale-105 transition duration-300">
    </div>

    <!-- Konten About -->
    <div class="flex flex-col px-10 gap-4">
      <h2 class="text-3xl font-bold text-cyan-400">About Me</h2>
      <p class="text-blue-100 text-sm">Student • Developer • Explorer • Gamer</p>
      <p class="text-gray-300 leading-relaxed text-xl">
        I'm <span class="text-cyan-300 font-semibold">Syahrul Ridho R. Rauf</span>, an enthusiastic developer who loves building creative and useful tech products. Currently, I'm focusing on web development, machine learning, and mapping technologies.
      </p>
      <p class="text-blue-100 text-sm">SMK Negeri 1 Limboto • Universitas Negeri Gorontalo</p>
      <p class="text-blue-100 text-sm">Kota Gorontalo, Gorontalo, Indonesia</p>
    </div>
  </div>
  <div class="ml-16 max-w-screen flex flex-col lg:flex-row items-center">
    <h2 class="text-3xl font-bold text-cyan-400">Educational Background</h2>
  </div>
</div>
</template>

<style scoped>

</style>