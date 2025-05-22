// Sidebar.vue
<script setup>
import { ref, onMounted, onUnmounted } from 'vue' // computed tidak terpakai, bisa dihapus jika tidak ada case lain
import ListNav from './ListNav.vue'
import logoAsset from '../assets/logo.png'

const barItems = ref([
  { label: 'Welcome', href: '#welcome', iconName: 'home', iconPath: 'M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6' },
  { label: 'About', href: '#about', iconName: 'information-circle', iconPath: 'M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z' },
  { label: 'Skill', href: '#skill', iconName: 'sparkles', iconPath: 'M5 3v4M3 5h4M5 11v4h4M19 3v4h-4M19 11v4h-4M12 5V3M12 11V9M12 19v-2M9 3.5H7.5V5M14.5 3.5H17V5M9 19h4M7.5 16.5l1.5 1.5 1.5-1.5M14.5 16.5l1.5 1.5 1.5-1.5' },
  { label: 'Project', href: '#project', iconName: 'collection', iconPath: 'M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10' },
  { label: 'Contact', href: '#contact', iconName: 'mail', iconPath: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' },
]);

const sectionElements = ref([]);
const activeSectionHref = ref(barItems.value.length > 0 ? barItems.value[0].href : '');

// Fungsi yang diperbarui untuk mendapatkan index section aktif
function getActiveSectionIndexBasedOnView() {
  if (!sectionElements.value || sectionElements.value.length === 0) {
    return 0;
  }

  let activeIndex = 0; // Default ke section pertama
  // Titik fokus di viewport, misalnya 25% dari atas. Section yang paling dekat dengan ini akan dianggap aktif.
  const focalPointY = window.innerHeight * 0.25; 
  let minDistanceToFocalPoint = Infinity;

  sectionElements.value.forEach((section, index) => {
    if (section) {
      const rect = section.getBoundingClientRect();
      // Section dianggap kandidat jika setidaknya sebagian ada di viewport
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

// Fungsi untuk update href section aktif berdasarkan scroll
function updateActiveSectionOnScroll() {
  const currentIndex = getActiveSectionIndexBasedOnView(); // Menggunakan fungsi baru
  if (barItems.value[currentIndex] && activeSectionHref.value !== barItems.value[currentIndex].href) {
    activeSectionHref.value = barItems.value[currentIndex].href;
  } else if (barItems.value.length > 0 && activeSectionHref.value === '' && currentIndex === 0) {
    // Inisialisasi jika belum ada yang aktif dan section pertama terdeteksi
    activeSectionHref.value = barItems.value[0].href;
  }
}

// Debounce (tetap sama)
function debounce(func, delay) {
  let timeout;
  return function(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}
const debouncedUpdateActiveSection = debounce(updateActiveSectionOnScroll, 100);

onMounted(() => {
  sectionElements.value = barItems.value
    .map(item => item.href && document.getElementById(item.href.substring(1)))
    .filter(el => el !== null);
  
  window.addEventListener('scroll', debouncedUpdateActiveSection, { passive: true }); // { passive: true } untuk performa
  updateActiveSectionOnScroll(); // Pengecekan awal
});

onUnmounted(() => {
  window.removeEventListener('scroll', debouncedUpdateActiveSection);
});

// Fungsi Navigasi Scroll Kanan (modifikasi untuk update highlight instan)
function scrollToSection(index, updateActiveImmediately = false) {
  if (sectionElements.value[index]) {
    sectionElements.value[index].scrollIntoView({ behavior: 'smooth', block: 'start' });
    if (updateActiveImmediately && barItems.value[index]) {
      // Langsung update highlight agar UI terasa lebih responsif saat tombol diklik
      activeSectionHref.value = barItems.value[index].href;
    }
  }
}

function scrollToPreviousSection() {
  if (!sectionElements.value.length) return;
  // Gunakan fungsi yang diupdate untuk mendapatkan index saat ini dengan benar
  const currentIndex = getActiveSectionIndexBasedOnView(); 
  const prevIndex = Math.max(0, currentIndex - 1);

  if (currentIndex === 0 && prevIndex === 0) {
    // Jika sudah di section pertama, cek apakah benar-benar di puncak halaman
    // Ini mencegah scroll jika sudah di puncak dan tombol atas ditekan lagi
    if (sectionElements.value[0] && sectionElements.value[0].getBoundingClientRect().top < -10) { // Beri sedikit toleransi
         scrollToSection(prevIndex, true);
    }
  } else {
      scrollToSection(prevIndex, true);
  }
}

function scrollToNextSection() {
  if (!sectionElements.value.length) return;
  const currentIndex = getActiveSectionIndexBasedOnView();
  const nextIndex = Math.min(sectionElements.value.length - 1, currentIndex + 1);

  if (currentIndex === sectionElements.value.length - 1 && nextIndex === currentIndex) {
     // Jika sudah di section terakhir, cek apakah benar-benar di bagian bawah halaman
     if (sectionElements.value[currentIndex]) {
        const currentRect = sectionElements.value[currentIndex].getBoundingClientRect();
        const isAtPageBottom = (window.innerHeight + window.scrollY) >= document.body.offsetHeight - 10; // Toleransi 10px
        // Cek jika bagian bawah section terakhir masih terlihat di atas bagian bawah viewport
        if (currentRect.bottom > window.innerHeight + 10 && !isAtPageBottom) { 
             scrollToSection(nextIndex, true);
        }
     }
  } else {
    scrollToSection(nextIndex, true);
  }
}

</script>

<template>
  <div 
    class="group fixed top-0 left-0 h-screen z-[100] w-16 hover:w-64 transition-all duration-300 ease-in-out bg-gradient-to-b from-slate-950 via-indigo-950 to-purple-950 shadow-2xl shadow-purple-500/30 border-r border-purple-700/50"
  >
    <div class="h-full px-3 py-4 overflow-y-auto flex flex-col">
      <div class="mb-8 flex justify-center items-center h-12">
        <img :src="logoAsset" alt="Logo" class="w-10 h-10 bg-white/10 backdrop-blur-sm rounded-full p-1 group-hover:hidden transition-opacity duration-200">
      </div>
      <div class="hidden group-hover:block mb-5 pl-1 transition-opacity duration-300 delay-100">
        <img :src="logoAsset" alt="Logo" class="w-10 h-10 bg-white/10 backdrop-blur-sm rounded-full p-1 mb-2">
        <h1 class="text-indigo-100 text-base font-bold leading-tight">
          Syahrul R. Rauf
        </h1>
        <p class="text-purple-300 text-xs">Portofolio</p>
      </div>
      
      <ListNav :items="barItems" :active-item-href="activeSectionHref" class="flex-grow" />
      
      <div class="mt-auto pt-6 text-xs text-purple-400/70">
        <p class="text-center group-hover:text-left group-hover:pl-1">
          &copy; {{ new Date().getFullYear() }} 
          <span class="hidden group-hover:inline">
            <a href="https://github.com/syrauff" class="hover:underline hover:text-purple-300">syrauff</a>.
          </span>
        </p>
        <p class="hidden group-hover:block group-hover:pl-1">All Rights Reserved.</p>
      </div>
    </div>
  </div>

  <div class="fixed h-screen z-[90] top-0 right-0 flex flex-col justify-center items-center w-16 sm:w-20 pointer-events-none">
    <div class="flex flex-col items-center space-y-3 pointer-events-auto">
      <button @click="scrollToPreviousSection" aria-label="Scroll to previous section" class="text-purple-300/70 hover:text-purple-100 p-2.5 rounded-full hover:bg-purple-700/50 transition-all transform hover:scale-110 active:scale-95">
        <svg class="w-5 h-5 sm:w-6 sm:h-6" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7 7.674 1.3a.91.91 0 0 0-1.348 0L1 7"/>
        </svg>
      </button>
      <div class="w-0.5 h-12 sm:h-16 bg-gradient-to-b from-transparent via-purple-500/70 to-transparent"></div>
      <button @click="scrollToNextSection" aria-label="Scroll to next section" class="text-purple-300/70 hover:text-purple-100 p-2.5 rounded-full hover:bg-purple-700/50 transition-all transform hover:scale-110 active:scale-95">
        <svg class="w-5 h-5 sm:w-6 sm:h-6" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 8">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="m1 1 5.326 5.7a.909.909 0 0 0 1.348 0L13 1"/>
        </svg>
      </button>
    </div>
  </div>
</template>

<style scoped>
/* Pastikan text-indigo-100, text-purple-300, dll. sesuai dengan palet warna Anda */
/* atau gunakan kelas warna standar Tailwind. */

/* Styling untuk ListNav mungkin perlu disesuaikan di dalam komponen ListNav.vue */
/* agar rata kiri dan menampilkan ikon dengan benar saat sidebar expanded. */

/* Untuk efek smooth pada margin-left konten utama saat sidebar hover */
/* Div wrapper konten utama harus ada di luar komponen ini jika sidebar adalah komponen global, */
/* atau Anda perlu mengatur struktur aplikasi Anda sehingga class ml-16/ml-64 bisa diterapkan */
/* pada wrapper konten utama Anda. */
/* Saya telah menambahkan div wrapper sementara untuk konten utama di template ini. */
</style>