<script setup>
import faceicon from '../assets/facegen.png'

// defineProps(['items']) // 'items' tidak digunakan di template ini, bisa dihapus jika tidak relevan
</script>

<template>
  <section 
    id="welcome" 
    class="min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-slate-900 via-gray-900 to-slate-950 text-white p-6 sm:p-10 relative overflow-hidden"
  >
    <div class="w-full max-w-6xl flex flex-col md:flex-row items-center justify-center gap-8 md:gap-12 z-10">
      
      <div class="md:w-2/5 flex justify-center md:justify-end shrink-0">
        <img 
          :src="faceicon" 
          class="h-60 w-60 sm:h-72 sm:w-72 md:h-80 md:w-80 object-cover rounded-full shadow-2xl shadow-purple-500/40 transition-all duration-500 ease-in-out hover:scale-105 hover:shadow-cyan-400/50 transform hover:rotate-3" 
          alt="Syahrul R. Rauf" 
        />
        </div>

      <div class="md:w-3/5 flex flex-col items-center md:items-start text-center md:text-left">
        <p class="text-lg sm:text-xl md:text-2xl mb-1 sm:mb-2 font-light text-indigo-300">
          Hello, I'm <span class="font-semibold text-cyan-300 drop-shadow-[0_0_5px_rgba(56,189,248,0.7)]">Syahrul...</span>
        </p>
        <h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-extrabold mb-4 sm:mb-6 leading-tight tracking-tight ">
          "Life like a <span class="text-cyan-400">Game</span>.
          I can <span class="text-green-400 hover:text-green-300 transition-colors">Win</span>, I can <span class="text-red-400 hover:text-red-300 transition-colors">Lose</span>.
          But how about draw? Haha, I don't know!"
        </h1>
        <p class="text-md sm:text-lg text-purple-200/90 mb-3 sm:mb-4">
          I'm a <span class="font-semibold">Student</span> and Aspiring <span class="font-semibold">Developer</span>.
        </p>
        <p class="text-sm sm:text-base text-gray-300 leading-relaxed max-w-xl">
          Welcome to my personal portfolio. Here, I will introduce who I am, my skills, and some of the projects I have worked on. Feel free to explore this page to get to know me better. Want to connect? Let's contact me!
        </p>
      </div>

    </div>
    
    <div class="absolute top-0 left-0 w-full h-full overflow-hidden pointer-events-none z-0">
        </div>
  </section>
</template>

<style scoped>
/* Styling untuk Text Shadow jika diperlukan kustomisasi lebih lanjut dari plugin Tailwind */
/* Kelas text-shadow-md dan text-shadow-blue-400 dari kode Anda mungkin memerlukan plugin Tailwind seperti tailwindcss-textshadow */
/* Jika tidak menggunakan plugin, Anda bisa definisikan di sini atau menggunakan drop-shadow utility */
.text-cyan-300.drop-shadow-\[0_0_5px_rgba\(56\,189\,248\,0\.7\)\] {
  filter: drop-shadow(0 0 5px rgba(56,189,248,0.7));
}

h1 { /* Sedikit efek bayangan halus pada judul utama */
  text-shadow: 0px 2px 15px rgba(128, 90, 213, 0.3); /* Warna ungu halus */
}
</style>