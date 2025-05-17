<script setup>
import ListNav from "./ListNav.vue";
import logo from "../assets/logo.png";

const navItems = [
  { label: 'Welcome', href: '#welcome' },
  { label: 'About', href: '#about' },
  { label: 'Skill', href: '#skill' },
  { label: 'Project', href: '#project' },
  { label: 'Contact', href: '#contact' },
]
</script>

<template>
  <nav class="bg-gradient-to-r from-cyan-200 to-blue-800  bord dark:bg-gray-900">
    <div class="items-center justify-between mx-auto py-2 px-32">
      <a href="#" class="flex items-center space-x-3 rtl:space-x-reverse">
          <img :src="logo" class="h-10" alt="Flowbite Logo" />
          <span class="self-center text-cyan-200 text-2xl  font-semibold whitespace-nowrap dark:text-white"></span>
      </a>
      <button data-collapse-toggle="navbar-default" type="button" class="inline-flex items-center p-2 w-10 h-10 justify-center text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600" aria-controls="navbar-default" aria-expanded="false">
          <span class="sr-only">Open main menu</span>
          <svg class="w-5 h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
              <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15"/>
          </svg>
      </button>
      <div class="hidden w-full md:block md:w-auto" id="navbar-default">
        <ListNav :items="navItems" />
      </div>
    </div>
  </nav>
</template>

<style scoped>

</style>