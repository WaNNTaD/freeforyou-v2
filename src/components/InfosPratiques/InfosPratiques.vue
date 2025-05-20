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
    gsap.from(locationCard.value, {
      scrollTrigger: {
        trigger: locationCard.value,
        start: 'top bottom-=100',
        toggleActions: 'play none none reverse',
      },
      x: -50,
      opacity: 0,
      duration: 0.8,
      ease: 'power2.out'
    });
    
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
      ease: 'power2.out'
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
      ease: 'power2.out'
    });
  }
});
</script>

<style scoped>
.infos-section {
  background: linear-gradient(135deg, var(--purple-deep) 0%, var(--purple-dark) 100%);
  position: relative;
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
  background: linear-gradient(to right, var(--orange-primary), var(--orange-quinary));
}

.infos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  margin-bottom: 60px;
}

.info-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(5px);
}

.info-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.icon {
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--orange-primary) 0%, var(--orange-quinary) 100%);
  color: white;
}

.icon svg {
  width: 30px;
  height: 30px;
}

h3 {
  font-size: 1.5rem;
  margin-bottom: 15px;
  color: white;
}

.info-card p {
  font-size: 1.1rem;
  margin-bottom: 0;
  color: rgba(255, 255, 255, 0.8);
}

ul {
  list-style: none;
  padding: 0;
  text-align: left;
  width: 100%;
}

li {
  margin-bottom: 10px;
  position: relative;
  padding-left: 25px;
  color: rgba(255, 255, 255, 0.8);
}

li::before {
  content: '•';
  position: absolute;
  left: 0;
  color: var(--orange-primary);
  font-size: 1.5rem;
  line-height: 1;
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
  background-color: #F44336;
  transform: translate(-50%, -50%);
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
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.3);
}

.map-container iframe {
  width: 100%;
  height: 100%;
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
