<script setup>
import photo from '../assets/foto.png' // Pastikan path ini benar
</script>

<template>
  <section 
    id="about" 
    class="min-h-screen flex flex-col items-center bg-gradient-to-br from-slate-900 via-gray-900 to-slate-950 text-white 
           px-4 sm:px-6 lg:px-8 
           pt-10 pb-12 sm:pt-24 sm:pb-16 md:pt-10 md:pb-20"
    >
    <div class="w-full max-w-5xl lg:max-w-6xl flex flex-col p-4 sm:p-6 md:p-8 rounded-2xl bg-slate-800/50 shadow-2xl shadow-sky-500/25 border border-slate-700/60">
      
      <div class="flex justify-center items-center mb-6 md:mb-6">
        <h2 class="text-3xl sm:text-4xl font-bold text-cyan-400 drop-shadow-[0_0_5px_rgba(56,189,248,0.6)]">
          About Me
        </h2>
      </div>
      
      <div class="flex flex-col md:flex-row items-center md:items-center gap-6 md:gap-8 lg:gap-12 mb-8 md:mb-8">
        <div class="shrink-0 text-center md:text-left">
          <img 
            :src="photo" 
            alt="My Photo" 
            class="w-40 h-40 sm:w-48 sm:h-48 md:w-60 md:h-64 object-cover object-top rounded-lg md:rounded-xl shadow-lg hover:scale-105 transition-transform duration-300 border-2 border-slate-600 hover:border-cyan-500/70"
          />
        </div>
        
        <div class="flex flex-col gap-3 md:pl-4 text-center md:text-left"> 
          <p class="text-gray-200 leading-relaxed text-base sm:text-lg">
            I'm <span class="text-cyan-300 font-semibold">Syahrul Ridho R. Rauf</span>, an enthusiastic developer who loves building creative and useful tech products. Currently, I'm focusing on web development, machine learning, and mapping technologies.
          </p>
          <p class="text-indigo-200 text-sm sm:text-base flex items-center justify-center md:justify-start gap-2">
            <svg class="inline w-5 h-5 text-sky-400 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 21a9 9 0 1 0 0-18 9 9 0 0 0 0 18Zm0 0a8.949 8.949 0 0 0 4.951-1.488A3.987 3.987 0 0 0 13 16h-2a3.987 3.987 0 0 0-3.951 3.512A8.948 8.948 0 0 0 12 21Zm3-11a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"/>
            </svg>
            <span>Now, I am <span class="text-sky-300 font-medium">Student • Developer • Explorer • Gamer</span></span>
          </p>
          <p class="text-indigo-200 text-sm sm:text-base flex items-center justify-center md:justify-start gap-2">
            <svg class="inline w-5 h-5 text-purple-300 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 13a3 3 0 1 0 0-6 3 3 0 0 0 0 6Z"/>
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.8 13.938h-.011a7 7 0 1 0-11.464.144h-.016l.14.171c.1.127.2.251.3.371L12 21l5.13-6.248c.194-.209.374-.429.54-.659l.13-.155Z"/>
            </svg>
            <span>I live in <span class="text-purple-200 font-medium">Kota Gorontalo, Gorontalo, Indonesia</span></span>
          </p>
        </div>
      </div>
      
      <div class="flex flex-col md:flex-row gap-6 md:gap-8 pt-6 md:pt-6 border-t border-slate-700/70"> 
        <div class="flex flex-col md:w-1/2 space-y-3"> 
          <h3 class="text-xl sm:text-2xl font-bold text-cyan-300 text-center md:text-left flex items-center justify-center md:justify-start gap-2">
            <svg class="inline w-7 h-7 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 20v-9l-4 1.125V20h4Zm0 0h8m-8 0V6.66667M16 20v-9l4 1.125V20h-4Zm0 0V6.66667M18 8l-6-4-6 4m5 1h2m-2 3h2"/>
            </svg>
            Education
          </h3>
          <div class="text-gray-300 text-sm space-y-1.5 pl-1 md:pl-0">
            <p>Saya telah menyelesaikan pendidikan saya di:</p>
            <ul class="list-none pl-2 space-y-1.5"> 
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>SD Muhammadiyah Kota Utara</li>
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>MTs. Negeri 1 Kota Gorontalo</li>
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>MAN Insan Cendekia Gorontalo</li>
            </ul>
            <p class="mt-3">dan sekarang saya sedang menempuh studi di:</p> 
            <ul class="list-none pl-2 space-y-1.5">
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>Universitas Negeri Gorontalo</li>
            </ul>
          </div>
        </div>
        
        <div class="flex flex-col md:w-1/2 space-y-3"> 
          <h3 class="text-xl sm:text-2xl font-bold text-cyan-300 text-center md:text-left flex items-center justify-center md:justify-start gap-2">
            <svg class="inline w-7 h-7 shrink-0" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5.35709 16V5.78571c0-.43393.34822-.78571.77777-.78571H18.5793c.4296 0 .7778.35178.7778.78571V16M5.35709 16h-1c-.55229 0-1 .4477-1 1v1c0 .5523.44771 1 1 1H20.3571c.5523 0 1-.4477 1-1v-1c0-.5523-.4477-1-1-1h-1M5.35709 16H19.3571M9.35709 8l2.62501 2.5L9.35709 13m4.00001 0h2"/>
            </svg>
            Experience
          </h3>
          <div class="text-gray-300 text-sm space-y-1.5 pl-1 md:pl-0">
            <p>Saya berpengalaman dalam pembuatan:</p>
            <ul class="list-none pl-2 space-y-1.5">
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>Diagram Flow Data</li>
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>Website</li>
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>Model Machine Learning</li>
              <li class="flex items-start"><span class="text-sky-400 mr-2 shrink-0 text-base">▸</span>Document</li>
            </ul>
          </div>
        </div>
      </div> 
    </div> 
  </section>
</template>

<style scoped>
/* Styling Anda yang sudah ada */
h1 { /* Ini merujuk pada h1 di WelcomeSection, bukan h2 di AboutSection. Mungkin perlu dikoreksi jika hanya untuk AboutSection */
  text-shadow: 0px 1px 3px rgba(var(--tw-shadow-color), 0.5), 0px 2px 8px rgba(var(--tw-shadow-color), 0.3);
  /* --tw-shadow-color: theme('colors.purple.500'); */
}
</style>