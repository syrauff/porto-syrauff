<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const projects = ref([
  {
    id: 1,
    title: "Aplikasi Manajemen Armada Galaksi",
    shortTitle: "ArmadaApp",
    image: "https://images.unsplash.com/photo-1518355079682-BN0tan?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
    description: "Sebuah aplikasi web komprehensif untuk melacak dan mengelola armada pesawat ruang angkasa antargalaksi. Dibangun dengan backend Laravel yang kuat, frontend Vue.js yang dinamis, dan styling modern menggunakan Tailwind CSS.",
    link: "#",
    tags: ["Web App", "Manajemen", "Full-stack"],
    tools: [
      { name: "Laravel", icon: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Laravel.svg/1200px-Laravel.svg.png" },
      { name: "Vue.js", icon: "https://vuejs.org/images/logo.png" },
      { name: "Tailwind CSS", icon: "https://upload.wikimedia.org/wikipedia/commons/d/d5/Tailwind_CSS_Logo.svg" },
      { name: "MySQL", icon: "https://www.mysql.com/common/logos/logo-mysql-170x115.png" },
      { name: "Inertia.js", icon: "https://inertiajs.com/assets/icon.png" },
    ],
  },
  {
    id: 2,
    title: "Jelajah Kosmos: Portofolio Interaktif",
    shortTitle: "Portofolio V3",
    image: "https://images.unsplash.com/photo-1446776811953-b23d57bd21aa?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
    description: "Portofolio pribadi yang didesain ulang dengan nuansa kosmik, menampilkan visualisasi 3D menggunakan Three.js dan dibangun di atas Nuxt.js untuk pengalaman pengguna yang imersif dan cepat.",
    link: "#",
    tags: ["Personal", "3D Web", "Interactive"],
    tools: [
      { name: "Nuxt.js", icon: "https://nuxtjs.org/logos/nuxt-icon-white.png" },
      { name: "Three.js", icon: "https://threejs.org/files/logo.svg" },
      { name: "Tailwind CSS", icon: "https://upload.wikimedia.org/wikipedia/commons/d/d5/Tailwind_CSS_Logo.svg" },
      { name: "GSAP", icon: "https://greensock.com/gsap-logomark.svg" }, // URL ikon GSAP diperbaiki
      { name: "Vercel", icon: "https://assets.vercel.com/image/upload/front/favicon/vercel/logomark.svg" },
    ],
  },
  {
    id: 3,
    title: "Detektor Anomali Sinyal Pulsar",
    shortTitle: "Pulsar Anomaly",
    image: "https://images.unsplash.com/photo-1582661099501-9aaa4Miscellaneous_Items_items?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1200&q=80",
    description: "Model Machine Learning untuk mendeteksi pola sinyal anomali dari data teleskop radio bintang pulsar. Dikembangkan menggunakan Python, TensorFlow, dan dielola dalam lingkungan Miniconda.",
    link: "#",
    tags: ["Machine Learning", "Astronomi", "Analisis Data"],
    tools: [
      { name: "Python", icon: "https://upload.wikimedia.org/wikipedia/commons/c/c3/Python-logo-notext.svg" },
      { name: "TensorFlow", icon: "https://upload.wikimedia.org/wikipedia/commons/thumb/2/2d/Tensorflow_logo.svg/1200px-Tensorflow_logo.svg.png" },
      { name: "Miniconda", icon: "https://docs.conda.io/en/latest/_images/conda_logo.svg" }, // URL ikon Conda/Miniconda diperbaiki
      { name: "Pandas", icon: "https://pandas.pydata.org/static/img/pandas.svg" },
      { name: "Matplotlib", icon: "https://matplotlib.org/_static/logo_dark.svg" },
    ],
  },
]);

const selectedProject = ref(null);
let autoCycleTimer = null;
const autoCycleDelay = 5000; // 5 detik
const isProjectAreaHovered = ref(false);

// Fungsi asli untuk mengganti data selectedProject
const _internalSelectProject = (project) => {
  selectedProject.value = project;
};

// Fungsi yang akan dipanggil oleh tombol atau auto-cycle
const selectProject = (project) => {
  stopAutoCycle(); // Hentikan timer saat ada interaksi atau pergantian otomatis
  _internalSelectProject(project);
  startAutoCycle(); // Mulai lagi timer setelah proyek dipilih
};

const selectNextProject = () => {
  if (!selectedProject.value || projects.value.length <= 1) return;

  const currentIndex = projects.value.findIndex(p => p.id === selectedProject.value.id);
  const nextIndex = (currentIndex + 1) % projects.value.length;
  selectProject(projects.value[nextIndex]);
};

function startAutoCycle() {
  stopAutoCycle(); // Pastikan tidak ada duplikat timer
  if (!isProjectAreaHovered.value && projects.value.length > 1) {
    autoCycleTimer = setTimeout(() => {
      selectNextProject();
      // selectProject yang dipanggil oleh selectNextProject akan memanggil startAutoCycle lagi
    }, autoCycleDelay);
  }
}

function stopAutoCycle() {
  if (autoCycleTimer) {
    clearTimeout(autoCycleTimer);
    autoCycleTimer = null;
  }
}

const handleProjectAreaEnter = () => {
  isProjectAreaHovered.value = true;
  stopAutoCycle();
};

const handleProjectAreaLeave = () => {
  isProjectAreaHovered.value = false;
  startAutoCycle();
};

onMounted(() => {
  if (projects.value.length > 0) {
    // Langsung pilih proyek pertama dan mulai siklus
    selectProject(projects.value[0]);
  }
});

onUnmounted(() => {
  stopAutoCycle();
});

</script>

<template>
  <section 
    id="project"
    class="h-screen flex flex-col bg-gradient-to-br from-[#000011] via-[#0c0c2c] to-[#120328] text-gray-200 overflow-hidden"
  >
    <div class="flex flex-col h-full w-full max-w-7xl mx-auto p-4 sm:p-6 lg:p-8">

      <header class="shrink-0 pb-6 md:pb-8 text-center">
        <h1 class="text-3xl sm:text-4xl md:text-5xl font-bold tracking-tight">
          My <span class="text-purple-400 drop-shadow-[0_0_10px_rgba(192,132,252,0.7)]">Galactic Projects</span>
        </h1>
      </header>

      <main class="flex-grow flex flex-col lg:flex-row w-full gap-6 lg:gap-8 overflow-hidden">
        <div 
          v-if="selectedProject" 
          :key="selectedProject.id" 
          class="flex flex-col lg:flex-row w-full h-full gap-6 lg:gap-8 overflow-hidden"
          @mouseenter="handleProjectAreaEnter"
          @mouseleave="handleProjectAreaLeave"
        >
          <section aria-labelledby="project-title" class="w-full lg:w-2/3 xl:w-3/4 flex flex-col group perspective bg-gray-900/60 backdrop-blur-lg rounded-xl shadow-2xl hover:shadow-[0_0_25px_rgba(168,85,247,0.4)] transition-all duration-500 transform-style-3d hover:scale-[1.01] overflow-hidden border border-purple-900/50 hover:border-purple-700/70">
            <div class="relative w-full h-48 sm:h-56 md:h-64 shrink-0">
              <img
                :src="selectedProject.image"
                :alt="selectedProject.title"
                class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105"
              >
              <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent"></div>
              <h2 id="project-title" class="absolute bottom-3 left-3 sm:bottom-4 sm:left-4 text-xl sm:text-2xl md:text-3xl font-bold text-white drop-shadow-lg">
                {{ selectedProject.title }}
              </h2>
            </div>
            <div class="p-4 sm:p-5 md:p-6 flex flex-col justify-between flex-grow overflow-y-auto custom-scrollbar-space">
              <p class="text-xs sm:text-sm text-gray-300 hover:text-gray-200 transition-colors mb-4 leading-relaxed">
                {{ selectedProject.description }}
              </p>
              <div class="mt-auto shrink-0 pt-2">
                <div class="flex flex-wrap gap-2 mb-4">
                    <span v-for="tag in selectedProject.tags" :key="tag" class="text-xs bg-purple-800/70 text-purple-300 px-2.5 py-1 rounded-full border border-purple-700/50 hover:bg-purple-700/70 hover:text-purple-200 transition-all">
                        {{ tag }}
                    </span>
                </div>
                <div class="text-right">
                    <a
                    :href="selectedProject.link"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="inline-block text-sm sm:text-base bg-purple-600 text-white px-4 py-2 sm:px-5 sm:py-2.5 rounded-lg hover:bg-purple-500 focus:ring-4 focus:ring-purple-600/50 transition-all duration-300 font-semibold shadow-md hover:shadow-lg transform hover:-translate-y-0.5 active:translate-y-0 border border-purple-500 hover:border-purple-400"
                    >
                    Launch Mission
                    </a>
                </div>
              </div>
            </div>
          </section>

          <aside aria-labelledby="tools-heading" class="w-full lg:w-1/3 xl:w-1/4 flex flex-col bg-gray-900/50 backdrop-blur-md rounded-xl shadow-xl overflow-hidden border border-blue-900/50 hover:border-blue-700/70 transition-colors">
            <h3 id="tools-heading" class="text-lg sm:text-xl font-semibold text-cyan-400 text-center shrink-0 bg-gray-900/70 backdrop-blur-sm p-3 sm:p-4 sticky top-0 z-10 shadow-sm border-b border-blue-800/60">
              Tech Constellation
            </h3>
            <div v-if="selectedProject.tools && selectedProject.tools.length > 0" class="grid grid-cols-3 lg:grid-cols-2 gap-x-2 gap-y-3 sm:gap-x-3 sm:gap-y-4 p-3 sm:p-4 overflow-y-auto custom-scrollbar-space flex-grow">
              <div v-for="tool in selectedProject.tools" :key="tool.name" class="flex flex-col items-center text-center group/tool">
                <div class="p-2 sm:p-3 bg-blue-950/60 rounded-lg group-hover/tool:bg-cyan-700/30 transition-colors duration-300 border border-blue-800/70 group-hover/tool:border-cyan-600/70">
                  <img
                    :src="tool.icon"
                    :alt="tool.name"
                    class="h-10 w-10 sm:h-12 sm:w-12 md:h-14 md:w-14 object-contain transition-all duration-300 group-hover/tool:scale-110 group-hover/tool:drop-shadow-[0_0_10px_rgba(34,211,238,0.7)]"
                  >
                </div>
                <span class="text-xs sm:text-sm text-gray-400 mt-1.5 sm:mt-2 group-hover/tool:text-cyan-300 transition-colors">
                  {{ tool.name }}
                </span>
              </div>
            </div>
            <p v-else class="text-gray-500 text-sm text-center p-5 flex-grow flex items-center justify-center">
              No tech signals detected.
            </p>
          </aside>
        </div>
        <div v-else class="flex items-center justify-center w-full h-full text-center text-gray-500 text-xl">
          <p>Scanning for project signals...</p>
        </div>
      </main>

      <footer v-if="projects.length > 1" class="shrink-0 pt-6 md:pt-8">
        <div class="flex justify-center space-x-2 sm:space-x-3 md:space-x-4 flex-wrap gap-y-3">
          <button
            v-for="project in projects"
            :key="project.id"
            @click="selectProject(project)"
            :class="['px-3 py-1.5 sm:px-4 sm:py-2 rounded-md text-xs sm:text-sm font-medium transition-all duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-opacity-75 border',
                     selectedProject && selectedProject.id === project.id ? 'bg-purple-500 text-white shadow-lg scale-105 border-purple-400 focus:ring-purple-300' : 'bg-gray-800 hover:bg-gray-700 text-gray-400 hover:text-gray-200 border-gray-700 hover:border-gray-600 focus:ring-purple-500']"
          >
            {{ project.shortTitle || project.title }}
          </button>
        </div>
      </footer>

    </div>
  </section>
</template>

<style scoped>
.perspective {
  perspective: 1000px;
}
.transform-style-3d {
  transform-style: preserve-3d;
}

.custom-scrollbar-space::-webkit-scrollbar {
  width: 7px;
  height: 7px;
}
.custom-scrollbar-space::-webkit-scrollbar-track {
  background-color: rgba(17, 24, 39, 0.5); /* gray-900/50 */
  border-radius: 10px;
}
.custom-scrollbar-space::-webkit-scrollbar-thumb {
  background-color: #8b5cf6; /* purple-500 */
  border-radius: 10px;
  border: 1px solid rgba(30, 20, 50, 0.8);
}
.custom-scrollbar-space::-webkit-scrollbar-thumb:hover {
  background-color: #a78bfa; /* purple-400 */
}
</style>