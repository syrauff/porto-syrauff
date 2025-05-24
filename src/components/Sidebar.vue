<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import ListNav from './ListNav.vue'; // Anda perlu menyesuaikan komponen ini
import logoAsset from '../assets/logo.png';

const barItems = ref([
  { label: 'Welcome', href: '#welcome', iconName: 'home', iconPath: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' },
  { label: 'About', href: '#about', iconName: 'information-circle', iconPath: 'M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z' },
  { label: 'Skill', href: '#skill', iconName: 'sparkles', iconPath: 'M5 3v4M3 5h4M5 11v4h4M19 3v4h-4M19 11v4h-4M12 5V3M12 11V9M12 19v-2M9 3.5H7.5V5M14.5 3.5H17V5M9 19h4M7.5 16.5l1.5 1.5 1.5-1.5M14.5 16.5l1.5 1.5 1.5-1.5' },
  { label: 'Project', href: '#project', iconName: 'collection', iconPath: 'M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10' },
  { label: 'Contact', href: '#contact', iconName: 'mail', iconPath: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' },
]);

const sectionElements = ref([]);
const activeSectionHref = ref(barItems.value.length > 0 ? barItems.value[0].href : '');

function getActiveSectionIndexBasedOnView() {
  if (!sectionElements.value || sectionElements.value.length === 0) return 0;
  let activeIndex = 0;
  const focalPointY = window.innerHeight * 0.25; 
  let minDistanceToFocalPoint = Infinity;
  sectionElements.value.forEach((section, index) => {
    if (section) {
      const rect = section.getBoundingClientRect();
      const isPartiallyInView = rect.top < window.innerHeight && rect.bottom > 0;
      if (isPartiallyInView) {
        const distance = Math.abs(rect.top - focalPointY);
        if (distance < minDistanceToFocalPoint) {
          minDistanceToFocalPoint = distance;
          activeIndex = index;
        }
      }
    }
  });
  return activeIndex;
}



onMounted(() => {
  sectionElements.value = barItems.value
    .map(item => item.href && document.getElementById(item.href.substring(1)))
    .filter(el => el !== null);
  
});

onUnmounted(() => {
  window.removeEventListener('scroll', debouncedUpdateActiveSection);
});

function scrollToSection(index) {
  if (sectionElements.value[index] && barItems.value[index]) {
    const targetSection = sectionElements.value[index];
    activeSectionHref.value = barItems.value[index].href; // Update highlight
    targetSection.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
}

function handleNavItemClick(href) {
  const itemIndex = barItems.value.findIndex(item => item.href === href);
  if (itemIndex !== -1) {
    scrollToSection(itemIndex);
  }
}

function scrollToPreviousSection() {
  if (!sectionElements.value.length) return;
  const currentViewIndex = getActiveSectionIndexBasedOnView(); 
  let targetIndex = currentViewIndex > 0 ? currentViewIndex - 1 : 0;
  scrollToSection(targetIndex, true);
}

function scrollToNextSection() {
  if (!sectionElements.value.length) return;
  const currentViewIndex = getActiveSectionIndexBasedOnView();
  let targetIndex = currentViewIndex < sectionElements.value.length - 1 ? currentViewIndex + 1 : sectionElements.value.length - 1;
  scrollToSection(targetIndex, true);
}
</script>

<template>
  <div 
    class="group fixed z-[100] transition-all duration-300 ease-in-out shadow-2xl
           bg-gradient-to-b from-slate-950 via-indigo-950 to-purple-950 
           md:top-0 md:left-0 md:h-screen md:w-16 md:hover:w-64 md:border-r md:border-purple-700/50 md:shadow-purple-500/30
           bottom-0 left-0 w-full h-16 border-t border-purple-700/50 flex md:flex-col"
           >
    <div class="h-full w-full flex md:flex-col overflow-hidden
                px-2 md:px-3 py-1 md:py-4 
                items-center md:items-stretch 
                md:justify-normal justify-around md:overflow-y-auto"
    >
      <div class="hidden md:flex mb-8 justify-center items-center h-12 shrink-0">
        <img :src="logoAsset" alt="Logo" class="w-10 h-10 bg-white/10 backdrop-blur-sm rounded-full p-1 md:group-hover:hidden transition-opacity duration-200">
      </div>
      <div class="hidden md:group-hover:block mb-5 pl-1 transition-opacity duration-300 delay-100 shrink-0">
        <img :src="logoAsset" alt="Logo" class="w-10 h-10 bg-white/10 backdrop-blur-sm rounded-full p-1 mb-2">
        <h1 class="text-indigo-100 text-base font-bold leading-tight">
          Syahrul R. Rauf
        </h1>
        <p class="text-purple-300 text-xs">Portofolio</p>
      </div>
      
      <ListNav 
        :items="barItems" 
        :active-item-href="activeSectionHref" 
        @item-click="handleNavItemClick" 
        class="flex flex-row md:flex-col md:flex-grow overflow-x-auto md:overflow-x-hidden custom-horizontal-scrollbar-mobile md:custom-vertical-scrollbar" 
        />
      
      <div class="hidden md:block mt-auto pt-6 text-xs text-purple-400/70 shrink-0">
        <p class="text-center md:group-hover:text-left md:group-hover:pl-1">
          &copy; {{ new Date().getFullYear() }} 
          <span class="hidden md:group-hover:inline">
            <a href="https://github.com/syrauff" class="hover:underline hover:text-purple-300">syrauff</a>.
          </span>
        </p>
        <p class="hidden md:group-hover:block md:group-hover:pl-1">All Rights Reserved.</p>
      </div>
    </div>
  </div>

  <div class="fixed z-[90] top-0 right-0 h-[calc(100vh-4rem)] md:h-screen flex flex-col justify-center items-center 
              w-12 sm:w-16 pointer-events-none">
    <div class="flex flex-col items-center space-y-3 pointer-events-auto">
      <button @click="scrollToPreviousSection" aria-label="Scroll to previous section" class="text-purple-300/70 hover:text-purple-100 p-2 sm:p-2.5 rounded-full hover:bg-purple-700/50 transition-all transform hover:scale-110 active:scale-95">
        <svg class="w-4 h-4 sm:w-5 sm:h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7 7.674 1.3a.91.91 0 0 0-1.348 0L1 7"/>
        </svg>
      </button>
      <div class="w-0.5 h-10 sm:h-12 bg-gradient-to-b from-transparent via-purple-500/70 to-transparent"></div>
      <button @click="scrollToNextSection" aria-label="Scroll to next section" class="text-purple-300/70 hover:text-purple-100 p-2 sm:p-2.5 rounded-full hover:bg-purple-700/50 transition-all transform hover:scale-110 active:scale-95">
        <svg class="w-4 h-4 sm:w-5 sm:h-5" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 5.326 5.7a.909.909 0 0 0 1.348 0L13 1"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<style scoped>

</style>