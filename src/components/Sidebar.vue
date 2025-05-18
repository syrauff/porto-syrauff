<script setup>
import { ref } from 'vue'
import ListNav from './ListNav.vue'
import ListBar from './ListBar.vue'
import photo from '../assets/foto.png'
import logo from '../assets/logo.png'

const isSidebarOpen = ref(false)
const barItems = [
  { label: 'Welcome', href: '#welcome' },
  { label: 'About', href: '#about' },
  { label: 'Skill', href: '#skill' },
  { label: 'Project', href: '#project' },
  { label: 'Contact', href: '#contact' },
]

function toggleSidebar() {
  isSidebarOpen.value = !isSidebarOpen.value
}
</script>

<template>

<div class="relative">
    <div class="group fixed top-0 left-0 h-screen z-50 w-16 hover:w-64 transition-all duration-300 ease-in-out bg-white dark:bg-gray-800 shadow-lg">
        <div class="h-full px-3 py-4 overflow-y-auto border border-r-blue-700 bg-blue-950  dark:bg-gray-800 flex flex-col justify-between">
            <!-- <img :src="photo" alt="foto" class="h-36 border rounded-full mb-4 mx-auto" /> -->
            <img :src="logo" alt="" class="group-hover:hidden bg-white rounded-full">
            <h1 class="hidden group-hover:block text-amber-50 text-center text-l font-bold">Protofolio <br> Syahrul Ridho R Rauf</h1>
            <ListNav :items="barItems" />
            <p class="group-hover:hidden text-sm text-gray-500 dark:text-gray-400 text-center mt-4">
                &copy;<a href="https://github.com/syrauff" class="hover:underline">syrauff</a>
            </p>
            <p class="hidden group-hover:block text-sm text-gray-500 dark:text-gray-400 text-center mt-4">
                &copy; 2025 <a href="https://github.com/syrauff" class="hover:underline">syrauff</a>. All Rights Reserved.
            </p>
        </div>

    </div>
    <div class="fixed h-screen z-50 top-0 right-0 flex flex-col justify-center items-center w-20 ">
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