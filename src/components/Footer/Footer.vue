<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-content">
        <div class="footer-logo">
          <h2>FreeForY🖤U</h2>
          <p class="tagline">Drive Safe</p>
        </div>
        
        <div class="footer-links">
          <h3>Navigation</h3>
          <ul>
            <li><a href="#hero">Accueil</a></li>
            <li><a href="#infos">Infos Pratiques</a></li>
            <li><a href="#lineup">Line-up</a></li>
          </ul>
        </div>
        
        <div class="footer-socials">
          <!-- <h3>Suivez-nous</h3>
          <div class="social-icons">
            <a href="#" class="social-icon">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path>
              </svg>
            </a>
            <a href="#" class="social-icon">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
              </svg>
            </a>
          </div> -->
        </div>
      </div>
      
      <div class="back-to-top" @click="scrollToTop">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="18 15 12 9 6 15"></polyline>
        </svg>
      </div>
      
      <div class="copyright">
        <p>&copy; {{ currentYear }} FreeForY🖤U. Tous droits réservés.</p>
        <p class="disclaimer">Conduisez prudemment. Ne buvez pas si vous conduisez.</p>
      </div>
    </div>
    
    <div class="footer-wave">
      <svg data-name="Layer 1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 120" preserveAspectRatio="none">
        <path d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z" class="shape-fill"></path>
      </svg>
    </div>
    
    <!-- Éléments décoratifs -->
    <div class="footer-grid-decoration">
      <div class="footer-grid-line" v-for="i in 5" :key="i"></div>
    </div>
    <div class="footer-beat-decoration">
      <div class="footer-beat" v-for="i in 3" :key="i" :style="{ animationDelay: `${i * 0.4}s` }"></div>
    </div>
    <div class="footer-glow"></div>
  </footer>
</template>

<script setup>
import { computed, ref, onMounted } from 'vue';

// Année courante pour le copyright
const currentYear = computed(() => new Date().getFullYear());

// Référence pour les animations
const footerRef = ref(null);

// Fonction pour remonter en haut de la page
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};

onMounted(() => {
  // Animation du bouton back-to-top
  const backToTopButton = document.querySelector('.back-to-top');
  
  if (backToTopButton) {
    gsap.from(backToTopButton, {
      y: 50,
      opacity: 0,
      duration: 1,
      delay: 0.5,
      ease: 'power3.out'
    });
    
    // Effet de rebond au survol
    backToTopButton.addEventListener('mouseenter', () => {
      gsap.to(backToTopButton, {
        y: -5,
        duration: 0.3,
        ease: 'power2.out'
      });
    });
    
    backToTopButton.addEventListener('mouseleave', () => {
      gsap.to(backToTopButton, {
        y: 0,
        duration: 0.3,
        ease: 'power2.out'
      });
    });
  }
  
  // Animation du logo
  const logo = document.querySelector('.footer-logo h2');
  if (logo) {
    gsap.fromTo(logo,
      { scale: 0.9, opacity: 0.5 },
      {
        scrollTrigger: {
          trigger: '.footer-logo',
          start: 'top bottom-=100',
          toggleActions: 'play none none none'
        },
        scale: 1,
        opacity: 1,
        duration: 1.5,
        ease: 'elastic.out(1, 0.5)'
      }
    );
  }
});
</script>

<style scoped>
.footer {
  background: linear-gradient(135deg, var(--toxic-night) 0%, var(--blood-depth) 100%);
  color: white;
  position: relative;
  padding: 120px 0 40px;
  margin-top: 80px;
  box-shadow: inset 0 0 100px rgba(0, 0, 0, 0.6);
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAABmJLR0QA/wD/AP+gvaeTAAAA30lEQVRoge3aMQrCQBhF4TdWFhY2XsHCwmtY2ngmW8HL2HgOm80JDCwiTDZmxvwfpAp5782wLARJkiRJkgYFrIAt8MxkC6yApm9kzbmRi4auQasmVsBj4MgNqPuOXQ0cOgMXYA50wD5zurePcTdw1hk4A7PM6d4+xt3AWWfgo+/YBWgzpnv7Nzd9xyZJugfD30JSPZbIqchYIqciY4mciowlcioyXyXS8P3yvwBzfmfMO89kB9Tf7jRW1cCRM7DJnO7tY9wNnPUZOQFFxqTvYIyKnJH/+xcY60JJkiRJ+g9vQbQH3th4OQUAAAAASUVORK5CYII=);
  opacity: 0.03;
  pointer-events: none;
  z-index: 1;
}

.footer-wave {
  position: absolute;
  top: -70px;
  left: 0;
  width: 100%;
  overflow: hidden;
  line-height: 0;
  transform: rotate(180deg);
  filter: drop-shadow(0 -5px 15px rgba(0, 255, 102, 0.2));
}

.footer-wave svg {
  position: relative;
  display: block;
  width: calc(100% + 1.3px);
  height: 70px;
}

.footer-wave .shape-fill {
  fill: var(--toxic-night);
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
  margin-bottom: 40px;
  position: relative;
  z-index: 5;
}

.footer-logo h2 {
  font-size: 2.5rem;
  margin: 0;
  background: linear-gradient(to right, var(--acid-burn), var(--shock-purple));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 
    0 0 10px rgba(0, 255, 102, 0.7),
    0 0 20px rgba(0, 255, 102, 0.3);
  animation: neon-pulse 4s infinite alternate;
}

.tagline {
  margin-top: 5px;
  color: rgba(255, 255, 255, 0.8);
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.8);
}

@keyframes neon-pulse {
  0% {
    text-shadow: 
      0 0 5px rgba(0, 255, 102, 0.5),
      0 0 15px rgba(0, 255, 102, 0.3);
  }
  100% {
    text-shadow: 
      0 0 10px rgba(188, 19, 254, 0.6),
      0 0 20px rgba(188, 19, 254, 0.4);
  }
}

.footer-links h3,
.footer-socials h3 {
  font-size: 1.3rem;
  margin-bottom: 15px;
  color: white;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
  position: relative;
  display: inline-block;
}

.footer-links h3:after,
.footer-socials h3:after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 50%;
  height: 1px;
  background: var(--acid-burn);
  box-shadow: 0 0 8px var(--acid-burn);
}

.footer-links ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 15px;
  position: relative;
}

.footer-links a {
  color: rgba(255, 255, 255, 0.8);
  transition: all 0.3s ease;
  text-decoration: none;
  position: relative;
  padding-left: 18px;
  text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
}

.footer-links a:before {
  content: '>';
  position: absolute;
  left: 0;
  color: var(--acid-burn);
  font-size: 0.9rem;
  text-shadow: 0 0 5px var(--acid-burn);
  transition: transform 0.3s ease;
}

.footer-links a:hover {
  color: var(--acid-burn);
  transform: translateX(3px);
  text-shadow: 0 0 10px rgba(0, 255, 102, 0.4);
  text-decoration: none;
}

.footer-links a:hover:before {
  transform: translateX(3px);
}

.social-icons {
  display: flex;
  gap: 15px;
}

.social-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.6);
  color: var(--acid-burn);
  transition: all 0.3s ease;
  border: 1px solid rgba(0, 255, 102, 0.2);
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.4);
}

.social-icon:hover {
  background: rgba(10, 10, 10, 0.8);
  color: var(--shock-purple);
  transform: translateY(-3px) scale(1.1);
  border-color: var(--shock-purple);
  box-shadow: 
    0 10px 20px rgba(0, 0, 0, 0.5),
    0 0 15px rgba(188, 19, 254, 0.3);
}

.social-icon svg {
  width: 18px;
  height: 18px;
  filter: drop-shadow(0 0 3px rgba(0, 255, 102, 0.6));
}

.back-to-top {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.7);
  color: var(--acid-burn);
  position: absolute;
  right: 30px;
  bottom: 100px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 
    0 5px 15px rgba(0, 0, 0, 0.4),
    0 0 20px rgba(0, 255, 102, 0.2);
  border: 1px solid rgba(0, 255, 102, 0.3);
  z-index: 10;
  animation: pulseButton 3s infinite alternate;
}

.back-to-top:hover {
  background: rgba(10, 10, 10, 0.8);
  transform: translateY(-5px);
  box-shadow: 
    0 10px 30px rgba(0, 0, 0, 0.6),
    0 0 30px rgba(0, 255, 102, 0.4);
}

.back-to-top svg {
  width: 25px;
  height: 25px;
  filter: drop-shadow(0 0 5px rgba(0, 255, 102, 0.8));
}

@keyframes pulseButton {
  0% {
    box-shadow: 
      0 5px 15px rgba(0, 0, 0, 0.4),
      0 0 20px rgba(0, 255, 102, 0.2);
  }
  100% {
    box-shadow: 
      0 5px 15px rgba(0, 0, 0, 0.5),
      0 0 25px rgba(188, 19, 254, 0.4);
  }
}

.copyright {
  text-align: center;
  margin-top: 30px;
  padding-top: 20px;
  border-top: 1px solid rgba(0, 255, 102, 0.1);
  position: relative;
  z-index: 5;
}

.copyright:before {
  content: '';
  position: absolute;
  top: -1px;
  left: 30%;
  width: 40%;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--acid-burn), transparent);
  box-shadow: 0 0 10px var(--acid-burn);
}

.copyright p {
  margin: 5px 0;
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
}

.disclaimer {
  font-weight: 500;
  color: var(--radiation) !important;
  text-shadow: 0 0 10px rgba(215, 254, 19, 0.4) !important;
  letter-spacing: 0.5px;
}

/* Éléments décoratifs */
.footer-grid-decoration {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  opacity: 0.1;
  z-index: 2;
}

.footer-grid-line {
  position: absolute;
  width: 1px;
  height: 100%;
  background: linear-gradient(to bottom, transparent, var(--acid-burn), transparent);
}

.footer-grid-line:nth-child(1) { left: 20%; animation: footerGridPulse 8s infinite ease-in-out alternate; }
.footer-grid-line:nth-child(2) { left: 40%; animation: footerGridPulse 10s infinite ease-in-out alternate-reverse; }
.footer-grid-line:nth-child(3) { left: 60%; animation: footerGridPulse 7s infinite ease-in-out alternate; }
.footer-grid-line:nth-child(4) { left: 80%; animation: footerGridPulse 12s infinite ease-in-out alternate-reverse; }
.footer-grid-line:nth-child(5) { left: 90%; animation: footerGridPulse 9s infinite ease-in-out alternate; }

@keyframes footerGridPulse {
  0% {
    opacity: 0.1;
    height: 70%;
  }
  50% {
    opacity: 0.3;
  }
  100% {
    opacity: 0.1;
    height: 100%;
  }
}

.footer-beat-decoration {
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-around;
  z-index: 2;
  opacity: 0.1;
  pointer-events: none;
  transform: translateY(-50%);
}

.footer-beat {
  height: 2px;
  width: 30%;
  background: var(--acid-burn);
  border-radius: 2px;
  animation: footerBeatPulse 3s ease-in-out infinite;
  box-shadow: 0 0 10px var(--acid-burn);
}

@keyframes footerBeatPulse {
  0%, 100% {
    opacity: 0.1;
  }
  50% {
    opacity: 0.4;
    box-shadow: 0 0 20px var(--shock-purple);
  }
}

.footer-glow {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 150px;
  background: radial-gradient(ellipse at center bottom, rgba(0, 255, 102, 0.15) 0%, transparent 70%);
  pointer-events: none;
  z-index: 2;
}

@media (max-width: 768px) {
  .footer {
    padding: 100px 0 30px;
  }
  
  .footer-content {
    text-align: center;
  }
  
  .footer-links h3:after,
  .footer-socials h3:after {
    left: 50%;
    transform: translateX(-50%);
  }
  
  .footer-links a {
    display: inline-block;
    padding-left: 0;
  }
  
  .footer-links a:before {
    content: none;
  }
  
  .social-icons {
    justify-content: center;
  }
  
  .back-to-top {
    right: 20px;
    bottom: 80px;
  }
}
</style>
