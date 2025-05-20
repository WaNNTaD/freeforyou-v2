<template>
  <section id="hero" class="hero-section section">
    <div class="particle-container" ref="particleContainer"></div>
    <div class="container hero-content">
      <div class="hero-text" ref="heroText">
        <h1>FreeForY🖤U</h1>
        <h2>Drive Safe</h2>
        <p>Une expérience musicale unique. À partir de 2h.</p>
      </div>
      <div class="scroll-indicator">
        <div class="mouse">
          <div class="wheel"></div>
        </div>
        <div class="arrow">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Références pour les animations
const particleContainer = ref(null);
const heroText = ref(null);

// Classe pour les particules
class Particle {
  constructor(canvas, ctx, options = {}) {
    this.canvas = canvas;
    this.ctx = ctx;
    this.x = options.x || Math.random() * canvas.width;
    this.y = options.y || Math.random() * canvas.height;
    this.vx = options.vx || (Math.random() - 0.5) * 0.5;
    this.vy = options.vy || (Math.random() - 0.5) * 0.5;
    this.radius = options.radius || Math.random() * 2 + 1;
    
    // Couleur aléatoire parmi notre nouvelle palette ultra-agressive
    const colors = [
      '#00FF66', '#FF0733', '#BC13FE', '#D7FE13', 
      '#00FF66', '#FF0733', '#BC13FE', '#FFFFFF',
      '#00FF66', '#FF0733'  // Plus de chances pour les couleurs principales
    ];
    this.color = options.color || colors[Math.floor(Math.random() * colors.length)];
    
    this.opacity = options.opacity || Math.random() * 0.5 + 0.1;
  }
  
  draw() {
    this.ctx.beginPath();
    this.ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
    this.ctx.fillStyle = this.color;
    this.ctx.globalAlpha = this.opacity;
    this.ctx.fill();
    this.ctx.closePath();
  }
  
  update() {
    this.x += this.vx;
    this.y += this.vy;
    
    // Rebond sur les bords
    if (this.x < 0 || this.x > this.canvas.width) {
      this.vx = -this.vx;
    }
    if (this.y < 0 || this.y > this.canvas.height) {
      this.vy = -this.vy;
    }
    
    this.draw();
  }
}

// Configuration du canvas et animation
let animationFrame;
let particles = [];
let canvas, ctx;
let mouseX = 0, mouseY = 0;

const initParticles = () => {
  if (!particleContainer.value) return;
  
  // Création du canvas
  canvas = document.createElement('canvas');
  ctx = canvas.getContext('2d');
  
  // Configuration canvas à la taille du conteneur
  const resizeCanvas = () => {
    canvas.width = particleContainer.value.offsetWidth;
    canvas.height = particleContainer.value.offsetHeight;
  };
  
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);
  
  // Ajout du canvas au DOM
  particleContainer.value.appendChild(canvas);
  
  // Création des particules
  const particleCount = Math.min(100, window.innerWidth / 10);
  for (let i = 0; i < particleCount; i++) {
    particles.push(new Particle(canvas, ctx));
  }
  
  // Suivi de la souris pour effet de parallaxe
  window.addEventListener('mousemove', (e) => {
    mouseX = e.clientX;
    mouseY = e.clientY;
  });
  
  // Animation
  const animate = () => {
    animationFrame = requestAnimationFrame(animate);
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    
    // Mise à jour et dessin des particules
    particles.forEach(particle => {
      particle.update();
    });
    
    // Effet de parallaxe subtil
    if (heroText.value) {
      const offsetX = (mouseX / window.innerWidth - 0.5) * 20;
      const offsetY = (mouseY / window.innerHeight - 0.5) * 20;
      
      gsap.to(heroText.value, {
        x: offsetX,
        y: offsetY,
        duration: 0.8,
        ease: 'power1.out'
      });
    }
  };
  
  animate();
};

// Animation du titre avec GSAP
const animateHeroText = () => {
  if (!heroText.value) return;
  
  const titleElements = heroText.value.querySelectorAll('h1, h2');
  
  gsap.from(titleElements, {
    y: 50,
    opacity: 0,
    stagger: 0.2,
    duration: 1,
    ease: 'power3.out'
  });
  
  gsap.from(heroText.value.querySelector('p'), {
    y: 30,
    opacity: 0,
    delay: 0.6,
    duration: 1,
    ease: 'power2.out'
  });
};

onMounted(() => {
  initParticles();
  animateHeroText();
});

onUnmounted(() => {
  if (animationFrame) {
    cancelAnimationFrame(animationFrame);
  }
  
  window.removeEventListener('resize', () => {});
  window.removeEventListener('mousemove', () => {});
});
</script>

<style scoped>
.hero-section {
  height: 100vh;
  min-height: 700px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  padding: 0;
}

.particle-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  padding: 0 20px;
}

.hero-text {
  max-width: 800px;
  margin: 0 auto;
}

h1 {
  font-size: 5rem;
  line-height: 1;
  margin: 0;
  background: linear-gradient(to right, var(--acid-burn), var(--shock-purple), var(--blood-scream));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 
    0 0 10px rgba(0, 255, 102, 0.7),
    0 0 20px rgba(0, 255, 102, 0.5),
    0 0 30px rgba(0, 255, 102, 0.3);
  animation: neon-pulse-title 4s infinite alternate;
}

@keyframes neon-pulse-title {
  0% {
    text-shadow: 
      0 0 10px rgba(0, 255, 102, 0.7),
      0 0 20px rgba(0, 255, 102, 0.5);
  }
  50% {
    text-shadow: 
      0 0 15px rgba(188, 19, 254, 0.7),
      0 0 25px rgba(188, 19, 254, 0.5),
      0 0 35px rgba(188, 19, 254, 0.3);
  }
  100% {
    text-shadow: 
      0 0 15px rgba(255, 7, 51, 0.7),
      0 0 25px rgba(255, 7, 51, 0.5),
      0 0 35px rgba(255, 7, 51, 0.3);
  }
}

h2 {
  font-size: 3rem;
  margin: 10px 0 30px;
  color: var(--text-primary);
  text-shadow: 
    0 2px 10px rgba(0, 0, 0, 0.8),
    0 0 20px rgba(188, 19, 254, 0.4);
  position: relative;
  display: inline-block;
}

h2::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 30%;
  width: 40%;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--acid-burn), transparent);
  box-shadow: 0 0 10px var(--acid-burn);
}

p {
  font-size: 1.5rem;
  max-width: 600px;
  margin: 0 auto;
  color: rgba(255, 255, 255, 0.9);
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.7);
  letter-spacing: 0.5px;
  position: relative;
  z-index: 2;
}

/* Animation de défilement */
.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeInUp 2s ease-in-out infinite;
}

.mouse {
  width: 26px;
  height: 40px;
  border: 2px solid var(--acid-burn);
  border-radius: 20px;
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
  box-shadow: 0 0 10px rgba(0, 255, 102, 0.5);
  position: relative;
  overflow: hidden;
}

.mouse::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle at center, rgba(0, 255, 102, 0.15) 0%, transparent 70%);
  pointer-events: none;
}

.wheel {
  width: 4px;
  height: 8px;
  background: var(--acid-burn);
  border-radius: 2px;
  margin-top: 8px;
  animation: scroll 1.5s ease infinite;
  box-shadow: 0 0 8px var(--acid-burn);
}

.arrow span {
  display: block;
  width: 10px;
  height: 10px;
  border-bottom: 2px solid var(--acid-burn);
  border-right: 2px solid var(--acid-burn);
  transform: rotate(45deg);
  margin: -5px;
  animation: arrowDown 1.5s ease infinite;
  box-shadow: 2px 2px 4px rgba(0, 255, 102, 0.5);
}

.arrow span:nth-child(2) {
  animation-delay: 0.2s;
}

.arrow span:nth-child(3) {
  animation-delay: 0.4s;
}

@keyframes scroll {
  0% {
    opacity: 1;
    transform: translateY(0);
  }
  100% {
    opacity: 0;
    transform: translateY(15px);
  }
}

@keyframes arrowDown {
  0% {
    opacity: 0;
    transform: rotate(45deg) translate(-5px, -5px);
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
    transform: rotate(45deg) translate(5px, 5px);
  }
}

@keyframes fadeInUp {
  0%, 100% {
    opacity: 0.5;
    transform: translate(-50%, 10px);
  }
  50% {
    opacity: 1;
    transform: translate(-50%, 0);
  }
}

@media (max-width: 768px) {
  h1 {
    font-size: 3.5rem;
  }
  
  h2 {
    font-size: 2rem;
  }
  
  p {
    font-size: 1.2rem;
  }
  
  .hero-section {
    min-height: 600px;
  }
}
</style>
