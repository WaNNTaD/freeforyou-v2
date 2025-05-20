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
    
    // Couleur aléatoire parmi notre palette
    const colors = [
      '#FF6D00', '#FF7900', '#FF8500', '#FF9100', '#FF9E00',
      '#240046', '#3C096C', '#5A189A', '#7B2CBF', '#9D4EDD'
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
  background: linear-gradient(to right, var(--orange-primary), var(--orange-quinary));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  text-shadow: 0 0 30px rgba(255, 109, 0, 0.3);
}

h2 {
  font-size: 3rem;
  margin: 10px 0 30px;
  color: white;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}

p {
  font-size: 1.5rem;
  max-width: 600px;
  margin: 0 auto;
  color: rgba(255, 255, 255, 0.9);
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
  border: 2px solid white;
  border-radius: 20px;
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}

.wheel {
  width: 4px;
  height: 8px;
  background: white;
  border-radius: 2px;
  margin-top: 8px;
  animation: scroll 1.5s ease infinite;
}

.arrow span {
  display: block;
  width: 10px;
  height: 10px;
  border-bottom: 2px solid white;
  border-right: 2px solid white;
  transform: rotate(45deg);
  margin: -5px;
  animation: arrowDown 1.5s ease infinite;
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
