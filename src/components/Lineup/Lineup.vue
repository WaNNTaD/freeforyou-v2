<template>
  <section id="lineup" class="lineup-section section">
    <div class="container">
      <h2 class="section-title">Line-up</h2>
      <div class="dj-grid">
        <div 
          v-for="(dj, index) in djs" 
          :key="index" 
          class="dj-card" 
          ref="djCards"
          @mouseenter="hoverDj(index)"
          @mouseleave="unhoverDj(index)">
          <div class="dj-avatar">
            <div class="avatar-circle">{{ dj.initial }}</div>
          </div>
          <h3>{{ dj.name }}</h3>
          <p v-if="dj.description">{{ dj.description }}</p>
          <div class="soundwave">
            <div class="bar" v-for="i in 20" :key="i"></div>
          </div>
        </div>
      </div>
    </div>
    <div class="vinyl-decoration" ref="vinyl">
      <div class="vinyl-inner"></div>
    </div>
    <div class="beats-decoration">
      <div class="beat" v-for="i in 10" :key="i" :style="{ animationDelay: `${i * 0.2}s` }"></div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const djs = ref([
  {
    name: 'ZKU',
    initial: 'Z',
    description: 'Ambiance électro unique et vibrante'
  },
  {
    name: 'Techsouye',
    initial: 'T',
    description: 'Beats techno et progressive house'
  },
  {
    name: 'Antoine',
    initial: 'A',
    description: 'Mélange de house et de disco rétro'
  }
]);

const djCards = ref([]);
const vinyl = ref(null);

// Animation lors du survol
const hoverDj = (index) => {
  if (djCards.value && djCards.value[index]) {
    const card = djCards.value[index];
    const soundwave = card.querySelector('.soundwave');
    
    gsap.to(card, {
      scale: 1.03,
      boxShadow: '0 15px 40px rgba(0, 0, 0, 0.3)',
      duration: 0.3
    });
    
    gsap.to(soundwave.querySelectorAll('.bar'), {
      height: () => 10 + Math.random() * 20,
      duration: 0.2,
      repeat: -1,
      yoyo: true,
      ease: 'power1.inOut',
      stagger: {
        each: 0.05,
        from: 'center'
      }
    });
  }
};

const unhoverDj = (index) => {
  if (djCards.value && djCards.value[index]) {
    const card = djCards.value[index];
    const soundwave = card.querySelector('.soundwave');
    
    gsap.to(card, {
      scale: 1,
      boxShadow: '0 5px 15px rgba(0, 0, 0, 0.2)',
      duration: 0.3
    });
    
    gsap.killTweensOf(soundwave.querySelectorAll('.bar'));
    gsap.to(soundwave.querySelectorAll('.bar'), {
      height: 3,
      duration: 0.2,
      stagger: {
        each: 0.02,
        from: 'center'
      }
    });
  }
};

onMounted(() => {
  // Animation du vinyle qui tourne
  if (vinyl.value) {
    gsap.to(vinyl.value, {
      rotation: 360,
      repeat: -1,
      duration: 10,
      ease: 'linear'
    });
  }
  
  // Animation des cartes DJ
  if (djCards.value.length) {
    djCards.value.forEach((card, index) => {
      gsap.from(card, {
        scrollTrigger: {
          trigger: card,
          start: 'top bottom-=100',
          toggleActions: 'play none none reverse'
        },
        y: 50,
        opacity: 0,
        duration: 0.8,
        delay: index * 0.15,
        ease: 'power2.out'
      });
    });
  }
});
</script>

<style scoped>
.lineup-section {
  background: linear-gradient(135deg, var(--purple-medium) 0%, var(--purple-light) 100%);
  position: relative;
  overflow: hidden;
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

.dj-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 30px;
  position: relative;
  z-index: 2;
}

.dj-card {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.dj-avatar {
  width: 120px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
  border-radius: 50%;
  background: rgba(0, 0, 0, 0.2);
  position: relative;
}

.avatar-circle {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--orange-primary) 0%, var(--orange-quinary) 100%);
  border-radius: 50%;
  font-size: 3rem;
  color: white;
  font-weight: bold;
}

h3 {
  font-size: 1.8rem;
  margin-bottom: 10px;
  color: white;
}

.dj-card p {
  font-size: 0.95rem;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 20px;
}

.soundwave {
  display: flex;
  align-items: flex-end;
  height: 40px;
  width: 100%;
  gap: 2px;
  justify-content: center;
}

.bar {
  width: 3px;
  height: 3px;
  background: var(--orange-primary);
  border-radius: 3px;
  transition: height 0.2s ease;
}

/* Éléments décoratifs */
.vinyl-decoration {
  position: absolute;
  width: 300px;
  height: 300px;
  background: radial-gradient(circle, #000 0%, #333 80%, #000 100%);
  border-radius: 50%;
  right: -100px;
  top: -100px;
  opacity: 0.2;
  z-index: 1;
}

.vinyl-inner {
  position: absolute;
  width: 100px;
  height: 100px;
  background: #ff9e00;
  border-radius: 50%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.beats-decoration {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: space-around;
  z-index: 1;
  opacity: 0.2;
}

.beat {
  width: 2px;
  height: 5px;
  background: white;
  border-radius: 2px;
  animation: beat 2s ease-in-out infinite;
}

@keyframes beat {
  0%, 100% {
    height: 5px;
  }
  50% {
    height: 30px;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }
  
  .dj-grid {
    grid-template-columns: 1fr;
  }
  
  .vinyl-decoration {
    width: 200px;
    height: 200px;
  }
  
  .vinyl-inner {
    width: 60px;
    height: 60px;
  }
}
</style>
