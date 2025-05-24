// ListNav.vue
<script setup>
defineProps({
  items: Array // Hanya menerima 'items'
})
// Definisikan emit untuk event klik
const emit = defineEmits(['item-click']);

function handleItemClick(href) {
  emit('item-click', href);
}
</script>

<template>
  <div class="flex flex-col w-full space-y-1">
    <a 
      v-for="item in items" 
      :key="item.label" 
      :href="item.href" 
      :aria-label="item.label"
      @click.prevent="handleItemClick(item.href)" :class="[
        'relative flex items-center p-3 rounded-md w-full transition-all duration-200 ease-in-out group/item justify-center group-hover:justify-start',
        item.href === activeItemHref 
          ? 'bg-purple-600 text-white shadow-lg scale-[1.02] ring-2 ring-purple-400 ring-offset-2 ring-offset-slate-950' // Gaya item aktif (dikontrol oleh Sidebar.vue)
          : 'text-purple-200/90 hover:bg-purple-700/70 hover:text-purple-50' 
      ]"
      >
      <svg 
        v-if="item.iconPath"
        class="w-5 h-5 sm:w-6 sm:h-6 shrink-0 stroke-current transition-colors duration-200 group-hover/item:text-purple-100"
        fill="none" 
        viewBox="0 0 24 24" 
        stroke-width="1.5" 
        xmlns="http://www.w3.org/2000/svg"
        aria-hidden="true"
      >
        <path stroke-linecap="round" stroke-linejoin="round" :d="item.iconPath" />
      </svg>
      <span v-else class="w-5 h-5 sm:w-6 sm:h-6 shrink-0 flex items-center justify-center text-xs font-bold text-purple-400">?</span>

      <span 
        class="ml-3 text-sm font-medium whitespace-nowrap
               hidden group-hover:inline-block
               opacity-0 group-hover:opacity-100
               transition-opacity duration-200 delay-150"
        >
        {{ item.label }}
      </span>

      <span 
        class="absolute left-full ml-4 px-2.5 py-1.5 text-xs font-medium text-indigo-100 bg-slate-900 
               border border-purple-700/80 rounded-md shadow-xl 
               opacity-0 scale-90 group-hover/item:opacity-100 group-hover/item:scale-100
               group-hover:hidden 
               transition-all duration-200 delay-75 
               pointer-events-none z-50 whitespace-nowrap"
      >
        {{ item.label }}
      </span>
    </a> 
  </div>
</template>


<style scoped>
/* Tidak ada style tambahan yang diperlukan jika Tailwind sudah benar. */
</style>