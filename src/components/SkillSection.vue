<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const props = defineProps({
  skills: {
    type: Array,
    default: () => [
      { id: 1, title: 'Web Frontend Dev', image: 'https://images.unsplash.com/photo-1605379399642-870262d3d051?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60', description: 'Antarmuka pengguna interaktif, responsif, dan intuitif dengan Vue.js, React, & Tailwind CSS.', detailsLink: '#' },
      { id: 2, title: 'Web Backend Dev', image: 'https://images.unsplash.com/photo-1542744173-8e7e53415bb0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60', description: 'Sisi server kuat & scalable, API, database, keamanan dengan Node.js, Python (Django/Flask).', detailsLink: '#' },
      { id: 3, title: 'Machine Learning & AI', image: 'https://images.unsplash.com/photo-1620712943543-bcc4688e7485?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60', description: 'Analisis prediktif, NLP, computer vision. TensorFlow, PyTorch, & Scikit-learn.', detailsLink: '#' },
      { id: 4, title: 'Sistem Analis & Desain', image: 'https://images.unsplash.com/photo-1517048676732-d65bc937f952?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60', description: 'Analisis kebutuhan bisnis, desain solusi software efektif, diagram alur, dokumentasi.', detailsLink: '#' },
      { id: 5, title: 'Mobile App Dev', image: 'https://images.unsplash.com/photo-1607252650355-f7fd0460ccdb?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=800&q=60', description: 'Pengembangan aplikasi mobile cross-platform dengan React Native atau Flutter.', detailsLink: '#' }
    ]
  },
  tools: {
    type: Array,
    default: () => [
      { name: 'JavaScript (ES6+)', icon: 'https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png' },
      { name: 'Python', icon: 'https://upload.wikimedia.org/wikipedia/commons/c/c3/Python-logo-notext.svg' },
      { name: 'Vue.js / Nuxt.js', icon: 'https://vuejs.org/images/logo.png' },
      { name: 'React / Next.js', icon: 'https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg' },
      { name: 'Node.js / Express', icon: 'https://nodejs.org/static/images/logo.svg' },
      { name: 'Tailwind CSS', icon: 'https://upload.wikimedia.org/wikipedia/commons/d/d5/Tailwind_CSS_Logo.svg'},
      { name: 'Docker', icon: 'https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png' },
      { name: 'Git & GitHub', icon: 'https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png' },
      { name: 'SQL / NoSQL DBs', icon: 'https://cdn-icons-png.flaticon.com/512/2906/2906209.png' },
      { name: 'Figma', icon: 'https://upload.wikimedia.org/wikipedia/commons/3/33/Figma-logo.svg' },
      { name: 'AWS / GCP', icon: 'https://upload.wikimedia.org/wikipedia/commons/9/93/Amazon_Web_Services_Logo.svg'},
      { name: 'Kubernetes', icon: 'https://upload.wikimedia.org/wikipedia/commons/3/39/Kubernetes_logo_without_workmark.svg'},
    ]
  }
});
const skillsContainerRef = ref(null);
const toolsContainerRef = ref(null);

function setupAutoScroll(containerRef, scrollStep = 0.5) {
  let animationFrameId = null;
  let isHovering = false;
  let direction = 1; // 1 untuk kanan, -1 untuk kiri

  const scrollLoop = () => {
    const el = containerRef.value;
    if (!el || isHovering) {
      animationFrameId = null;
      return;
    }

    const maxScrollLeft = el.scrollWidth - el.clientWidth;

    // Jika tidak ada yang bisa di-scroll, hentikan dan reset.
    if (maxScrollLeft <= 0.1) { // Toleransi kecil untuk floating point
      el.scrollLeft = 0; // Kembali ke awal jika tidak scrollable
      direction = 1;   // Reset arah
      animationFrameId = null;
      return;
    }

    // Logika scroll prediktif
    if (direction === 1) { // Bergerak ke kanan
      if (el.scrollLeft + scrollStep >= maxScrollLeft) {
        el.scrollLeft = maxScrollLeft; // Mentok di kanan
        direction = -1; // Balik arah
      } else {
        el.scrollLeft += scrollStep;
      }
    } else { // Bergerak ke kiri (direction === -1)
      if (el.scrollLeft - scrollStep <= 0) {
        el.scrollLeft = 0; // Mentok di kiri
        direction = 1; // Balik arah
      } else {
        el.scrollLeft -= scrollStep;
      }
    }

    animationFrameId = requestAnimationFrame(scrollLoop);
  };

  const handleMouseEnter = () => {
    isHovering = true;
    if (animationFrameId) {
      cancelAnimationFrame(animationFrameId);
      animationFrameId = null;
    }
  };

  const handleMouseLeave = () => {
    isHovering = false;
    // Mulai lagi hanya jika tidak ada frame yang berjalan dan bisa di-scroll
    // Pengecekan scrollWidth > clientWidth dilakukan di dalam checkAndRunScroll
    checkAndRunScroll(); 
  };

  // Fungsi untuk memeriksa apakah perlu scroll dan memulainya
  const checkAndRunScroll = () => {
    const el = containerRef.value;
    if (el && !isHovering) { // Hanya jalankan jika tidak di-hover
      if (el.scrollWidth > el.clientWidth + 0.1) { // Toleransi kecil
        if (!animationFrameId) { // Hanya mulai jika belum berjalan
          // Saat memulai/memulai ulang karena resize atau mouseleave,
          // kita bisa pertimbangkan untuk tidak mereset scrollLeft & direction
          // agar terasa lebih natural jika user baru saja mouseleave.
          // Namun, jika sebelumnya tidak scrollable dan sekarang scrollable, reset mungkin baik.
          // Untuk kasus ini, kita biarkan scrollLoop menangani posisi dan arah.
          animationFrameId = requestAnimationFrame(scrollLoop);
        }
      } else {
        // Jika tidak lagi scrollable, hentikan loop dan reset
        if (animationFrameId) {
          cancelAnimationFrame(animationFrameId);
          animationFrameId = null;
        }
        el.scrollLeft = 0; // Kembali ke awal
        direction = 1;   // Reset arah
      }
    } else if (el && isHovering && animationFrameId) {
        // Jika sedang dihover dan ada loop berjalan (seharusnya tidak terjadi karena handleMouseEnter)
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
    }
  };
  
  const debouncedCheckAndRunScroll = debounce(checkAndRunScroll, 200); // Debounce untuk resize

  onMounted(() => {
    const el = containerRef.value;
    if (el) {
      el.addEventListener('mouseenter', handleMouseEnter);
      el.addEventListener('mouseleave', handleMouseLeave);
      window.addEventListener('resize', debouncedCheckAndRunScroll);
      checkAndRunScroll(); // Pengecekan awal saat mount
    }
  });

  onUnmounted(() => {
    if (animationFrameId) {
      cancelAnimationFrame(animationFrameId);
    }
    const el = containerRef.value;
    if (el) {
      el.removeEventListener('mouseenter', handleMouseEnter);
      el.removeEventListener('mouseleave', handleMouseLeave);
    }
    window.removeEventListener('resize', debouncedCheckAndRunScroll);
  });
}

// Fungsi debounce sederhana (jika belum ada)
function debounce(func, delay) {
  let timeout;
  return function(...args) {
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(this, args), delay);
  };
}


// Inisialisasi tetap sama
setupAutoScroll(skillsContainerRef, 0.5);
setupAutoScroll(toolsContainerRef, 0.7);
</script>

<template>
  <section 
    id="skill" 
    class="h-screen flex flex-col bg-gradient-to-br from-slate-900 via-gray-900 to-slate-950 text-gray-200 overflow-hidden"
  >
    <div class="flex flex-col h-full w-full max-w-full mx-auto">

      <header class="shrink-0 pt-8 pb-6 md:pt-10 md:pb-8 text-center px-4">
        <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold tracking-tight">
          Core <span class="text-cyan-400 drop-shadow-[0_0_10px_rgba(34,211,238,0.6)]">Competencies</span>
        </h1>
      </header>

      <main class="flex-grow w-full flex flex-col space-y-8 md:space-y-10 overflow-hidden">
        
        <section id="skill-cards-carousel" aria-labelledby="skill-cards-heading" class="w-full lg:w-11/12 mx-auto pl-4 sm:pl-6 lg:pl-8 xl:pl-12 pr-1"> 
          <div ref="skillsContainerRef" class="flex overflow-x-auto space-x-5 md:space-x-6 pb-4 custom-horizontal-scrollbar">
            <div
              v-for="skill in props.skills"
              :key="skill.id"
              class="group bg-slate-800/70 backdrop-blur-md rounded-xl shadow-xl hover:shadow-cyan-500/30 transition-all duration-300 flex flex-col overflow-hidden border border-slate-700 hover:border-cyan-600/70 transform hover:-translate-y-1 w-72 sm:w-80 md:w-[340px] shrink-0"
            >
              <div class="relative w-full h-40 sm:h-44 shrink-0 overflow-hidden">
                <img :src="skill.image" :alt="skill.title" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105">
                <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-slate-900/50 to-transparent opacity-80 group-hover:opacity-100 transition-opacity duration-300"></div>
              </div>
              <div class="p-4 sm:p-5 flex flex-col justify-between flex-grow">
                <div>
                  <h2 class="text-lg sm:text-xl font-semibold text-transparent bg-clip-text bg-gradient-to-r from-sky-400 to-cyan-300 mb-2 group-hover:text-cyan-300 transition-colors truncate">
                    {{ skill.title }}
                  </h2>
                  <p class="text-xs sm:text-sm text-gray-400 group-hover:text-gray-300 transition-colors leading-relaxed flex-grow mb-3 line-clamp-3">
                    {{ skill.description }}
                  </p>
                </div>
                <div v-if="skill.detailsLink && skill.detailsLink !== '#'" class="mt-auto text-right pt-1">
                  <a :href="skill.detailsLink" class="inline-block text-xs sm:text-sm bg-cyan-600 text-white px-3 py-1.5 sm:px-4 sm:py-2 rounded-md hover:bg-cyan-500 focus:ring-2 focus:ring-cyan-400 focus:ring-opacity-50 transition-all duration-300 font-medium shadow-md hover:shadow-lg">
                    Detail
                  </a>
                </div>
              </div>
            </div>
            <div class="shrink-0 w-4 sm:w-6 lg:w-8 xl:w-12"></div>
          </div>
        </section>

        <section id="tools-carousel" aria-labelledby="tools-heading" class="w-full flex flex-col items-center pt-4 md:pt-6 pb-4 md:pb-6">
          <h2 id="tools-heading" class="text-xl md:text-2xl font-semibold text-center mb-5 md:mb-6 px-4">
            <span class="text-teal-400 drop-shadow-[0_0_8px_rgba(45,212,191,0.5)]">Toolbox</span> & Frameworks
          </h2>
          <div class="w-full lg:w-11/12 mx-auto pl-4 sm:pl-6 lg:pl-8 xl:pl-12 pr-1">
            <div ref="toolsContainerRef" class="flex items-center overflow-x-auto space-x-4 sm:space-x-5 md:space-x-6 pb-4 custom-horizontal-scrollbar justify-start md:justify-center">
              <div
                v-for="tool in props.tools"
                :key="tool.name"
                class="group relative p-3 sm:p-3.5 bg-slate-800/80 backdrop-blur-sm rounded-lg hover:bg-teal-700/40 transition-all duration-300 border border-slate-700 hover:border-teal-600/60 shrink-0"
                :title="tool.name"
              >
                <img :src="tool.icon" :alt="tool.name" class="h-10 w-10 sm:h-11 sm:w-11 md:h-12 md:w-12 object-contain transition-transform duration-300 group-hover:scale-110 group-hover:filter group-hover:brightness-125">
                <span class="absolute -bottom-2 left-1/2 -translate-x-1/2 bg-teal-600 text-white text-[10px] sm:text-xs px-1.5 py-0.5 rounded-md opacity-0 group-hover:opacity-100 group-hover:translate-y-2.5 transition-all duration-300 shadow-lg whitespace-nowrap z-10 pointer-events-none">
                  {{ tool.name }}
                </span>
              </div>
              <div class="shrink-0 w-4 sm:w-6 lg:w-8 xl:w-12"></div>
            </div>
          </div>
        </section>
      </main>
    </div>
  </section>
</template>

<style scoped>
.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.custom-horizontal-scrollbar::-webkit-scrollbar {
  height: 8px;
}
.custom-horizontal-scrollbar::-webkit-scrollbar-track {
  background-color: rgba(15, 23, 42, 0.4); /* slate-900/40 */
  border-radius: 10px;
}
.custom-horizontal-scrollbar::-webkit-scrollbar-thumb {
  background-color: #0891b2; /* cyan-700 */
  border-radius: 10px;
  border: 1px solid rgba(30, 41, 59, 0.6); /* slate-800 */
}
.custom-horizontal-scrollbar::-webkit-scrollbar-thumb:hover {
  background-color: #06b6d4; /* cyan-600 */
}

.custom-horizontal-scrollbar {
  scrollbar-width: thin;
  scrollbar-color: #0891b2 rgba(15, 23, 42, 0.4); /* thumb track - Untuk Firefox */
}
</style>