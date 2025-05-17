<script setup>

defineProps(['items'])

</script>

<template>
  <div id="project" class="flex flex-col items-center justify-center min-h-screen bg-gray-100 dark:bg-gray-900">
    <h1 class="text-4xl font-bold text-gray-800 dark:text-white">My Projects</h1>
    <p class="mt-4 text-lg text-gray-600 dark:text-gray-400">
      Here are some of the projects I have worked on.
    </p>
    <div class="mt-8 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
      <div v-for="item in items" :key="item.id" class="bg-white dark:bg-gray-800 p-4 rounded shadow">
        <h2 class="text-xl font-semibold text-gray-800 dark:text-white">{{ item.name }}</h2>
        <p class="mt-2 text-gray-600 dark:text-gray-400">{{ item.description }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>