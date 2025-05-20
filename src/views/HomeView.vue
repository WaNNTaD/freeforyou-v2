<template>
  <div class="home">
    <Header />
    <Hero />
    <InfosPratiques />
    <Lineup />
    <Footer />
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import Header from '../components/Header/Header.vue';
import Hero from '../components/Hero/Hero.vue';
import InfosPratiques from '../components/InfosPratiques/InfosPratiques.vue';
import Lineup from '../components/Lineup/Lineup.vue';
import Footer from '../components/Footer/Footer.vue';

onMounted(() => {
  // Initialisation des animations GSAP pour le scroll
  const sections = document.querySelectorAll('.section');
  
  sections.forEach(section => {
    gsap.fromTo(section, 
      { 
        opacity: 0,
        y: 100 
      }, 
      {
        opacity: 1,
        y: 0,
        duration: 1,
        scrollTrigger: {
          trigger: section,
          start: 'top bottom-=100',
          end: 'top center',
          toggleActions: 'play none none reverse',
          // markers: true, // Utile pour le débogage
        }
      }
    );
  });
});
</script>

<style scoped>
.home {
  overflow-x: hidden;
}
</style>

<style scoped>
.home {
  overflow-x: hidden;
  width: 100%;
}
</style>
