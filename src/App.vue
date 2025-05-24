<script setup>
import HelloWorld from './components/HelloWorld.vue'
import Navbar from './components/Navbar.vue'
import Sidebar from './components/Sidebar.vue'
import WelcomeSection from './components/WelcomeSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillSection from './components/SkillSection.vue'
import ProjectSection from './components/ProjectSection.vue'
import ContactSection from './components/ContactSection.vue'
</script>

<template>
  <div class="flex overflow-hidden h-screen"> <Sidebar />

    <main class="w-full md:ml-16 overflow-y-auto custom-page-scrollbar h-full"> 
      <section id="welcome">
        <WelcomeSection />
      </section>
      <section id="about">
        <AboutSection />
      </section>
      <section id="skill">
        <SkillSection />
      </section>
      <section id="project">
        <ProjectSection />
      </section>
      <section id="contact">
        <ContactSection />
      </section>
    </main>
  </div>
</template>

<style scoped>

main.custom-page-scrollbar { /* Atau selector lain yang menargetkan <main> Anda */
  scroll-behavior: smooth;
}
</style>