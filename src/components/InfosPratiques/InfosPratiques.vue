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
                <svg class="waze-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48">
                  <path fill="#2196F3" d="M13.3,21.3c0,1.5,1.2,2.7,2.7,2.7s2.7-1.2,2.7-2.7s-1.2-2.7-2.7-2.7S13.3,19.8,13.3,21.3z"/>
                  <path fill="#2196F3" d="M29.3,21.3c0,1.5,1.2,2.7,2.7,2.7s2.7-1.2,2.7-2.7s-1.2-2.7-2.7-2.7S29.3,19.8,29.3,21.3z"/>
                  <path fill="#2196F3" d="M23.3,14.9c-9.4-0.3-13.1-1.4-13.7-1.5c-0.1,0-0.1-0.1-0.1-0.1c0,0,0-0.1,0.1-0.1c0.1,0,2.3-1,5-1.1c0,0,0.1,0,0.1,0.1c0,0.1-0.1,0.2-0.1,0.2c0,0-0.1,0.1-0.2,0c-1.9,0.1-3.6,0.6-4.5,0.8c1.7,0.3,5.3,0.9,13.2,1.1c0,0,0.1,0,0.1,0.1v0.2C23.3,14.8,23.3,14.9,23.3,14.9z"/>
                  <path fill="#2196F3" d="M10.7,14.1c0,0-0.1-0.1-0.2-0.1c-0.3,0-0.4,0.2-0.4,0.3c0,0.1,0.1,0.6,1.2,0.7h0.1c1.1,0,2.3-0.5,2.3-0.5c0,0,0.1,0,0.1,0.1c0,0,0,0.1-0.1,0.1c-0.1,0-1.6,0.7-2.8,0.4c-0.7-0.2-0.9-0.5-0.9-0.8c0-0.3,0.3-0.6,0.7-0.6c0.1,0,0.2,0,0.3,0.1c0,0,0,0.1,0,0.2C10.7,14,10.7,14.1,10.7,14.1z"/>
                  <path fill="#2196F3" d="M38.7,18.7c0,0.1-0.1,0.2-0.3,0.2h-0.1c-0.1,0-28.7-4.2-29.2-4.3c-0.1,0-0.1-0.1-0.1-0.2c0-0.1,0.1-0.2,0.2-0.2c0,0,0,0,0.1,0c0.5,0.1,29.2,4.3,29.3,4.3C38.6,18.6,38.7,18.7,38.7,18.7z"/>
                  <path fill="#2196F3" d="M32.7,34.2c0,0-6.7,4.3-16.6,0c0,0-2.3-1-3.5-3.7L4.1,17.9c-0.1-0.1-0.1-0.3,0-0.4c0.3-0.2,3.2-2.9,3.9-4.1h7.6c0.2,0,0.4-0.2,0.4-0.4c0-0.2-0.2-0.4-0.4-0.4l0,0H8c-0.3,0-0.6-0.3-0.6-0.6s0.3-0.6,0.6-0.6h8.4c0.5,0,0.9,0.4,0.9,0.9s-0.4,0.9-0.9,0.9H8.8c-0.2,0.3-0.8,0.9-1.5,1.6c-0.4,0.4-0.8,0.7-1,0.9l8.3,12.2c1,2.4,3.1,3.2,3.1,3.2C26.6,37.4,32.7,34.2,32.7,34.2z"/>
                  <path fill="#2196F3" d="M16.6,22.8c0,0.4-0.3,0.6-0.6,0.6c-0.4,0-0.6-0.3-0.6-0.6c0-0.4,0.3-0.6,0.6-0.6C16.3,22.2,16.6,22.4,16.6,22.8z"/>
                  <path fill="#2196F3" d="M32.6,22.8c0,0.4-0.3,0.6-0.6,0.6c-0.4,0-0.6-0.3-0.6-0.6c0-0.4,0.3-0.6,0.6-0.6C32.3,22.2,32.6,22.4,32.6,22.8z"/>
                  <path fill="#2196F3" d="M43.8,17.9l-0.5,3.5C43,24.6,40.6,27,37.3,27h-2.1c-2.3,0-4.5,1-6,2.8l-5.7,6.6c-0.5,0.6-1.3,0.9-2.1,0.9c-0.9,0-1.7-0.4-2.3-1.1l-1.1-1.4c-0.2-0.3-0.2-0.8,0.1-1.1c0.3-0.2,0.8-0.2,1.1,0.1l1.1,1.4c0.3,0.3,0.8,0.3,1.1,0c1.8-2,3.5-4.2,5.5-6.5c1.8-2.1,4.5-3.3,7.3-3.3h2.1c2.5,0,4.2-1.7,4.5-3.7l0.4-3c0-0.3-0.2-0.6-0.5-0.6c-0.1,0-28.7-4.3-28.9-4.3c-0.3,0-0.6,0.2-0.6,0.5v0.1c0,0.3,0.2,0.6,0.5,0.6l8.9,1.3c0.1,0,0.2,0.1,0.2,0.1v0.1c0,0.1-0.1,0.3-0.2,0.3h-9.4c-0.5,0-1-0.4-1-0.8s0.4-0.8,0.9-0.9L40.7,16c1.6,0.2,2.8,1.6,2.8,3.3C43.6,17.7,43.9,17.6,43.8,17.9z"/>
                  <path fill="#F44336" d="M14 10 L38 34 M38 10 L14 34" stroke="red" stroke-width="4"/>
                </svg>
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

.waze-icon {
  width: 25px;
  height: 25px;
  margin-left: 10px;
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
