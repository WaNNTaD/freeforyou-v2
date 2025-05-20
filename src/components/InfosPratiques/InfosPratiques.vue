<template>
  <section id="infos" class="infos-section section">
    <div class="container">
      <h2 class="section-title">Infos Pratiques</h2>
      <div class="infos-grid">
        <div class="info-card location" ref="locationCard">
          <div class="icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
              <circle cx="12" cy="10" r="3"></circle>
            </svg>
          </div>
          <h3>Adresse</h3>
          <p>Rue Lisière du bois 16, 7063 Neufvilles</p>
        </div>

        <div class="info-card rules" ref="rulesCard">
          <div class="icon">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="12" y1="8" x2="12" y2="12"></line>
              <line x1="12" y1="16" x2="12.01" y2="16"></line>
            </svg>
          </div>
          <h3>Règles</h3>
          <ul>
            <li>Garez-vous intelligemment pour ne bloquer aucun véhicule.</li>
            <li>Pas d'achat de boisson sur place.</li>
            <li>Endroit prévu pour les mégots.</li>
            <li>
              <div class="no-waze">
                <span>Pas de Waze</span>
                <div class="waze-icon-container">
                  <img src="@/assets/images/waze-icon.png" alt="Logo Waze" class="waze-icon" />
                  <div class="waze-cross"></div>
                </div>
              </div>
            </li>
            <li>À partir de 2 h.</li>
          </ul>
        </div>
      </div>
      
      <div class="map-container" ref="mapContainer">
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d2543.8752575482224!2d4.019651776441666!3d50.59210857180779!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47c24f9227489d85%3A0x8e2c54f09456cedc!2sRue%20Lisi%C3%A8re%20du%20Bois%2016%2C%207063%20Soignies!5e0!3m2!1sfr!2sbe!4v1715165999999!5m2!1sfr!2sbe" 
          style="border:0;" 
          allowfullscreen="" 
          loading="lazy" 
          referrerpolicy="no-referrer-when-downgrade">
        </iframe>
      </div>
    </div>
    
    <!-- Éléments décoratifs -->
    <div class="grid-decoration" ref="gridDeco">
      <div class="grid-line" v-for="i in 10" :key="i"></div>
    </div>
    <div class="beat-decoration">
      <div class="beat" v-for="i in 5" :key="i" :style="{ animationDelay: `${i * 0.3}s` }"></div>
    </div>
    <div class="noise-overlay"></div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const locationCard = ref(null);
const rulesCard = ref(null);
const mapContainer = ref(null);

onMounted(() => {
  // Animation des cartes avec GSAP
  if (locationCard.value && rulesCard.value) {
    // Animation d'entrée pour la carte location
    gsap.from(locationCard.value, {
      scrollTrigger: {
        trigger: locationCard.value,
        start: 'top bottom-=100',
        toggleActions: 'play none none reverse',
      },
      x: -50,
      opacity: 0,
      duration: 0.8,
      ease: 'power3.out'
    });
    
    // Animation d'entrée pour la carte règles
    gsap.from(rulesCard.value, {
      scrollTrigger: {
        trigger: rulesCard.value,
        start: 'top bottom-=100',
        toggleActions: 'play none none reverse',
      },
      x: 50,
      opacity: 0,
      duration: 0.8,
      delay: 0.2,
      ease: 'power3.out'
    });
    
    // Animation des icônes
    gsap.to([locationCard.value.querySelector('.icon'), rulesCard.value.querySelector('.icon')], {
      scrollTrigger: {
        trigger: '.infos-grid',
        start: 'top center',
      },
      duration: 2,
      rotate: 360,
      ease: 'power1.inOut',
      repeat: 0,
    });
    
    // Animation du titre et de l'underline pour chaque carte
    [locationCard.value, rulesCard.value].forEach(card => {
      const h3 = card.querySelector('h3');
      if (h3) {
        gsap.to(h3, {
          scrollTrigger: {
            trigger: card,
            start: 'top center',
          },
          color: 'white',
          textShadow: '0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(255, 255, 255, 0.4)',
          duration: 1,
          ease: 'power2.out',
          yoyo: true,
          repeat: 1,
          repeatDelay: 0.5
        });
      }
    });
  }
  
  // Animation de la carte
  if (mapContainer.value) {
    gsap.from(mapContainer.value, {
      scrollTrigger: {
        trigger: mapContainer.value,
        start: 'top bottom-=100',
        toggleActions: 'play none none reverse',
      },
      y: 50,
      opacity: 0,
      duration: 0.8,
      delay: 0.4,
      ease: 'power3.out'
    });
    
    // Effet de scan sur la carte
    gsap.to(mapContainer.value, {
      scrollTrigger: {
        trigger: mapContainer.value,
        start: 'top center',
      },
      boxShadow: '0 15px 40px rgba(0, 0, 0, 0.6), 0 0 30px rgba(0, 255, 102, 0.3)',
      duration: 1,
      ease: 'power2.inOut',
      repeat: -1,
      yoyo: true
    });
  }
});
</script>

<style scoped>
.infos-section {
  background: linear-gradient(135deg, var(--toxic-night) 0%, var(--blood-depth) 100%);
  position: relative;
  overflow: hidden;
  box-shadow: inset 0 0 100px rgba(0, 0, 0, 0.6);
}

.section-title {
  text-align: center;
  font-size: 3rem;
  margin-bottom: 60px;
  color: white;
  position: relative;
}

.section-title:after {
  content: '';
  position: absolute;
  bottom: -15px;
  left: 50%;
  transform: translateX(-50%);
  width: 80px;
  height: 3px;
  background: linear-gradient(to right, var(--acid-burn), var(--shock-purple));
  box-shadow: 0 0 10px var(--acid-burn), 0 0 20px rgba(0, 255, 102, 0.3);
}

.infos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  margin-bottom: 60px;
}

.info-card {
  background: rgba(0, 0, 0, 0.7);
  border-radius: 15px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease, background 0.5s ease;
  border: 1px solid rgba(0, 255, 102, 0.2);
  backdrop-filter: blur(10px);
  box-shadow: 
    0 5px 15px rgba(0, 0, 0, 0.4),
    0 0 20px rgba(0, 255, 102, 0.1);
  position: relative;
  overflow: hidden;
}

.info-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5), 0 0 30px rgba(0, 255, 102, 0.2);
  background: rgba(10, 10, 10, 0.8);
}

.info-card:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, transparent, var(--acid-burn), transparent);
  animation: scanLine 2s linear infinite;
}

@keyframes scanLine {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

.icon {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--shock-purple) 0%, var(--blood-scream) 100%);
  color: white;
  box-shadow: 
    0 0 15px rgba(188, 19, 254, 0.5),
    0 0 30px rgba(188, 19, 254, 0.3),
    inset 0 0 15px rgba(0, 0, 0, 0.6);
  animation: pulseGlow 4s infinite alternate;
}

.icon svg {
  width: 35px;
  height: 35px;
  filter: drop-shadow(0 0 5px rgba(255, 255, 255, 0.8));
}

@keyframes pulseGlow {
  0% {
    box-shadow: 
      0 0 15px rgba(188, 19, 254, 0.5),
      0 0 30px rgba(188, 19, 254, 0.3);
  }
  100% {
    box-shadow: 
      0 0 20px rgba(255, 7, 51, 0.6),
      0 0 40px rgba(255, 7, 51, 0.4);
  }
}

h3 {
  font-size: 1.8rem;
  margin-bottom: 15px;
  color: white;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
  letter-spacing: 1px;
  position: relative;
  display: inline-block;
}

.info-card h3:after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--acid-burn);
  transition: width 0.4s ease;
}

.info-card:hover h3:after {
  width: 100%;
  box-shadow: 0 0 8px var(--acid-burn);
}

.info-card p {
  font-size: 1.1rem;
  margin-bottom: 0;
  color: rgba(255, 255, 255, 0.8);
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.8);
}

ul {
  list-style: none;
  padding: 0;
  text-align: left;
  width: 100%;
}

li {
  margin-bottom: 15px;
  position: relative;
  padding-left: 25px;
  color: rgba(255, 255, 255, 0.8);
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.8);
  transition: transform 0.2s ease, color 0.2s ease;
}

li:hover {
  color: var(--text-primary);
  transform: translateX(2px);
}

li::before {
  content: '•';
  position: absolute;
  left: 0;
  color: var(--acid-burn);
  font-size: 1.5rem;
  line-height: 1;
  text-shadow: 0 0 5px var(--acid-burn);
}

.no-waze {
  display: flex;
  align-items: center;
}

.waze-icon-container {
  position: relative;
  margin-left: 10px;
  width: 28px;
  height: 28px;
}

.waze-icon {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.waze-cross {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.waze-cross::before,
.waze-cross::after {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 140%;
  height: 3px;
  background-color: var(--blood-scream);
  transform: translate(-50%, -50%);
  box-shadow: 0 0 8px var(--blood-scream);
}

.waze-cross::before {
  transform: translate(-50%, -50%) rotate(45deg);
}

.waze-cross::after {
  transform: translate(-50%, -50%) rotate(-45deg);
}

.map-container {
  width: 100%;
  height: 400px;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5), 0 0 20px rgba(0, 255, 102, 0.1);
  border: 1px solid rgba(0, 255, 102, 0.2);
  position: relative;
}

.map-container:before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, var(--acid-burn), var(--shock-purple), var(--blood-scream));
  z-index: 10;
  box-shadow: 0 0 15px rgba(0, 255, 102, 0.5);
}

.map-container iframe {
  width: 100%;
  height: 100%;
}

/* Éléments décoratifs */
.grid-decoration {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  opacity: 0.1;
  z-index: 1;
  perspective: 800px;
}

.grid-line {
  position: absolute;
  height: 1px;
  width: 100%;
  background: linear-gradient(to right, transparent, var(--acid-burn), transparent);
}

.grid-line:nth-child(odd) {
  animation: gridPulse 6s infinite ease-in-out alternate;
}

.grid-line:nth-child(even) {
  animation: gridPulse 8s infinite ease-in-out alternate-reverse;
}

.grid-line:nth-child(1) { top: 10%; }
.grid-line:nth-child(2) { top: 20%; }
.grid-line:nth-child(3) { top: 30%; }
.grid-line:nth-child(4) { top: 40%; }
.grid-line:nth-child(5) { top: 50%; }
.grid-line:nth-child(6) { top: 60%; }
.grid-line:nth-child(7) { top: 70%; }
.grid-line:nth-child(8) { top: 80%; }
.grid-line:nth-child(9) { top: 90%; }
.grid-line:nth-child(10) { top: 95%; }

@keyframes gridPulse {
  0% {
    opacity: 0.1;
  }
  50% {
    opacity: 0.3;
  }
  100% {
    opacity: 0.1;
  }
}

.beat-decoration {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 100px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  z-index: 1;
  opacity: 0.2;
  pointer-events: none;
}

.beat {
  width: 30px;
  height: 2px;
  background: var(--acid-burn);
  border-radius: 2px;
  animation: beatPulse 2s ease-in-out infinite;
  box-shadow: 0 0 10px var(--acid-burn);
}

@keyframes beatPulse {
  0%, 100% {
    width: 30px;
  }
  50% {
    width: 80px;
  }
}

.noise-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAABmJLR0QA/wD/AP+gvaeTAAAA30lEQVRoge3aMQrCQBhF4TdWFhY2XsHCwmtY2ngmW8HL2HgOm80JDCwiTDZmxvwfpAp5782wLARJkiRJkgYFrIAt8MxkC6yApm9kzbmRi4auQasmVsBj4MgNqPuOXQ0cOgMXYA50wD5zurePcTdw1hk4A7PM6d4+xt3AWWfgo+/YBWgzpnv7Nzd9xyZJugfD30JSPZbIqchYIqciY4mciowlcioyXyXS8P3yvwBzfmfMO89kB9Tf7jRW1cCRM7DJnO7tY9wNnPUZOQFFxqTvYIyKnJH/+xcY60JJkiRJ+g9vQbQH3th4OQUAAAAASUVORK5CYII=);
  opacity: 0.03;
  pointer-events: none;
  z-index: 5;
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }
  
  .infos-grid {
    grid-template-columns: 1fr;
  }
  
  .map-container {
    height: 300px;
  }
}
</style>
