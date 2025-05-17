
<script setup>

defineProps(['items'])

</script>

<template>
  <div class="flex flex-col justify-center items-center">
    <a v-for="item in items" :key="item.label" :href="item.href" class="text-center md:inline-block py-2 px-2 text-cyan-200 rounded-sm border border-transparent hover:py-4 hover:text-cyan-50 md:hover:bg-transparent dark:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent hover:border hover:border-y-cyan-400 transition-all duration-200 ease-in-out" >
      {{ item.label }} 
    </a> 
  </div>
</template>

<style scoped>

</style>