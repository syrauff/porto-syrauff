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

</div>


</template>

<style scoped>

</style>