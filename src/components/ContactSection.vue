<script setup>
import { ref } from 'vue';

// defineProps(['items']) // 'items' tidak digunakan di template ini, bisa dihapus jika tidak relevan

// State untuk form input
const name = ref('');
const email = ref('');
const subject = ref('');
const message = ref('');

// State untuk status pesan form
const formStatus = ref({
  text: '',
  type: '', // 'success' atau 'error'
  active: false,
});

const handleSubmit = () => {
  // Validasi sederhana (bisa Anda kembangkan)
  if (!name.value || !email.value || !subject.value || !message.value) {
    formStatus.value = {
      text: 'Please fill in all required fields.',
      type: 'error',
      active: true,
    };
    // Sembunyikan pesan error setelah beberapa detik
    setTimeout(() => {
      formStatus.value.active = false;
    }, 5000);
    return;
  }

  // Di aplikasi nyata, Anda akan mengirim data ini ke server
  // Contoh: await fetch('/api/contact', { method: 'POST', body: JSON.stringify(...) });

  // Untuk demo ini, kita hanya tampilkan pesan sukses
  formStatus.value = {
    text: `Thank you for your message, ${name.value}! I'll get back to you soon.`,
    type: 'success',
    active: true,
  };

  // Reset form
  name.value = '';
  email.value = '';
  subject.value = '';
  message.value = '';

  // Sembunyikan pesan sukses setelah 5 detik
  setTimeout(() => {
    formStatus.value.active = false;
  }, 5000);
};

// Data untuk informasi kontak dan ikon sosial media (gunakan path SVG atau komponen ikon)
const contactDetails = ref([
  { label: 'Location', value: 'Kota Gorontalo, Indonesia', iconPath: 'M17.657 16.657L13.414 20.9a1.998 1.998 0 0 1-2.827 0l-4.244-4.243a8 8 0 1 1 11.314 0z M12 11a2 2 0 1 0 0-4 2 2 0 0 0 0 4z' }, // Location Pin
  { label: 'Email', value: 'syahrulrrrauf@gmail.com', iconPath: 'M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z' }, // Envelope
  { label: 'Phone', value: '+62 822 XXXX XXXX', iconPath: 'M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.308 1.154a11.034 11.034 0 005.37 5.37l1.154-2.308a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z' }  // Phone
]);

const socialLinks = ref([
  { name: 'LinkedIn', href: 'https://www.linkedin.com/in/syahrul-ridho-r-rauf/', iconPath: 'M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z M4 6.48A2.48 2.48 0 111.52 4 2.48 2.48 0 014 6.48z' }, // LinkedIn
  { name: 'GitHub', href: 'https://github.com/syrauff', iconPath: 'M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0012 18.13V22' }, // GitHub
  { name: 'Facebook', href: 'https://www.facebook.com/arul.rauf',  iconPath: 'M18 2h-3a5 5 0 00-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 011-1h3z' }, 
  { name: 'Instagram', href: 'https://www.instagram.com/rul_syh12', iconPath: 'M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.059 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948s-.014-3.667-.072-4.947c-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.948-.073zm0 5.838a3.736 3.736 0 100 7.472 3.736 3.736 0 000-7.472zm0 10.368a1.632 1.632 0 110-3.264 1.632 1.632 0 010 3.264z' } // Instagram
]);

const currentYear = new Date().getFullYear();

</script>

<template>
  <section 
    id="contact" 
    class="min-h-screen flex flex-col items-center justify-center bg-gradient-to-br from-slate-950 via-[#0A0A23] to-[#100320] text-gray-200 py-4 px-4 sm:px-6 lg:px-8"
  >
    <div class="w-full max-w-6xl mx-auto flex flex-col justify-center items-center space-y-2">

      <h1 class="text-4xl md:text-5xl font-extrabold text-center bg-clip-text text-transparent bg-gradient-to-r from-purple-400 via-pink-400 to-rose-400 drop-shadow-[0_0_10px_rgba(236,72,153,0.5)]">
        Get In Touch
      </h1>

      <p class="text-gray-300 text-center max-w-2xl text-base sm:text-lg">
        I'm always open to discussing new projects, creative ideas or opportunities to be part of your vision. Feel free to reach out!
      </p>

      <div class="w-full grid grid-cols-1 lg:grid-cols-3 gap-8 md:gap-10">
        
        <div class="bg-gray-900/50 backdrop-blur-lg border border-purple-800/60 rounded-2xl shadow-2xl shadow-purple-500/20 p-6 md:p-8 flex flex-col justify-between order-last lg:order-first">
          <div>
            <h2 class="text-xl sm:text-2xl font-semibold mb-6 text-purple-300">Contact Information</h2>
            <div class="space-y-5">
              <div v-for="detail in contactDetails" :key="detail.label" class="flex items-start space-x-3 group">
                <div class="bg-purple-600/20 p-3 rounded-full transition-all duration-300 group-hover:bg-purple-600/40 group-hover:scale-105">
                   <svg class="w-5 h-5 text-purple-300 group-hover:text-purple-100" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                        <path clip-rule="evenodd" fill-rule="evenodd" :d="detail.iconPath"></path>
                   </svg>
                </div>
                <div>
                  <h3 class="text-sm text-gray-400 group-hover:text-gray-300 transition-colors">{{ detail.label }}</h3>
                  <p class="text-base text-gray-200 group-hover:text-white transition-colors">{{ detail.value }}</p>
                </div>
              </div>
            </div>
          </div>

          <div class="mt-8 pt-6 border-t border-purple-800/50">
            <h3 class="text-lg font-medium mb-4 text-purple-300">Connect with me</h3>
            <div class="flex space-x-3">
              <a v-for="social in socialLinks" :key="social.name" :href="social.href" target="_blank" rel="noopener noreferrer" 
                 class="transition-all duration-300 transform hover:-translate-y-1 hover:scale-105 bg-purple-600/20 hover:bg-purple-600/40 p-3 rounded-full group"
                 :aria-label="`Connect with me on ${social.name}`">
                <svg class="w-5 h-5 text-purple-300 group-hover:text-purple-100" fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path :d="social.iconPath"></path>
                </svg>
              </a>
            </div>
          </div>
        </div>

        <div class="bg-gray-900/50 backdrop-blur-lg border border-sky-800/60 rounded-2xl shadow-2xl shadow-sky-500/20 p-6 md:p-8 lg:col-span-2">
          <h2 class="text-xl sm:text-2xl font-semibold mb-6 text-sky-300">Send Me a Message</h2>
          
          <div v-if="formStatus.active" 
               :class="[
                 'px-4 py-3 rounded-lg mb-4 text-sm transition-opacity duration-300',
                 formStatus.type === 'success' ? 'bg-green-500/20 border border-green-500/30 text-green-300' : '',
                 formStatus.type === 'error' ? 'bg-red-500/20 border border-red-500/30 text-red-300' : ''
               ]"
               role="alert">
            <p>{{ formStatus.text }}</p>
          </div>

          <form @submit.prevent="handleSubmit" class="space-y-5">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
              <div>
                <label for="name" class="block text-sm text-gray-300 mb-1.5">Your Name <span class="text-red-400">*</span></label>
                <input v-model="name" id="name" type="text" required class="w-full px-4 py-2.5 rounded-lg bg-slate-800/70 border border-slate-700 text-gray-200 focus:outline-none focus:bg-slate-700/90 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 transition-colors">
              </div>
              <div>
                <label for="email" class="block text-sm text-gray-300 mb-1.5">Your Email <span class="text-red-400">*</span></label>
                <input v-model="email" id="email" type="email" required class="w-full px-4 py-2.5 rounded-lg bg-slate-800/70 border border-slate-700 text-gray-200 focus:outline-none focus:bg-slate-700/90 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 transition-colors">
              </div>
            </div>

            <div>
              <label for="subject" class="block text-sm text-gray-300 mb-1.5">Subject <span class="text-red-400">*</span></label>
              <input v-model="subject" id="subject" type="text" required class="w-full px-4 py-2.5 rounded-lg bg-slate-800/70 border border-slate-700 text-gray-200 focus:outline-none focus:bg-slate-700/90 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 transition-colors">
            </div>

            <div>
              <label for="message" class="block text-sm text-gray-300 mb-1.5">Your Message <span class="text-red-400">*</span></label>
              <textarea v-model="message" id="message" rows="5" required class="w-full px-4 py-2.5 rounded-lg bg-slate-800/70 border border-slate-700 text-gray-200 resize-none focus:outline-none focus:bg-slate-700/90 focus:border-sky-500 focus:ring-1 focus:ring-sky-500 transition-colors"></textarea>
            </div>

            <div class="text-right pt-2">
              <button type="submit" class="px-6 py-3 rounded-lg font-semibold text-white bg-gradient-to-r from-sky-500 via-cyan-500 to-teal-500 hover:from-teal-500 hover:to-sky-500 transition-all shadow-lg hover:shadow-cyan-500/40 transform hover:-translate-y-0.5 active:scale-95">
                Send Message
              </button>
            </div>
          </form>
        </div>
      </div>

      <div class="text-center text-gray-500 text-xs mt-2 ">
        <p>© {{ currentYear }} syrauff. All rights reserved.</p>
      </div>

    </div>
  </section>
</template>

<style scoped>
/* Styling untuk drop-shadow pada judul utama jika diperlukan kustomisasi lebih lanjut */
/* atau jika Anda tidak menggunakan plugin text-shadow */
h1.drop-shadow-\[0_0_10px_rgba\(236\,72\,153\,0\.5\)\] {
  filter: drop-shadow(0 0 10px rgba(236,72,153,0.5)); /* Sesuaikan warna dengan gradient teks Anda */
}
</style>