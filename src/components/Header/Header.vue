<template>
  <header :class="{ 'header': true, 'header-scrolled': scrolled }">
    <div class="container">
      <div class="logo" ref="logoContainer">
        <h1 ref="logoTitle">FreeForY🖤U</h1>
      </div>
      <nav class="desktop-nav">
        <ul>
          <li><a href="#hero">Accueil</a></li>
          <li><a href="#infos">Infos Pratiques</a></li>
          <li><a href="#lineup">Line-up</a></li>
        </ul>
      </nav>
      <div class="mobile-menu-toggle" @click="toggleMobileMenu">
        <div :class="{ 'bar': true, 'animate': mobileMenuOpen }"></div>
        <div :class="{ 'bar': true, 'animate': mobileMenuOpen }"></div>
        <div :class="{ 'bar': true, 'animate': mobileMenuOpen }"></div>
      </div>
    </div>
    <div :class="{ 'mobile-menu': true, 'open': mobileMenuOpen }">
      <ul>
        <li><a href="#hero" @click="closeMobileMenu">Accueil</a></li>
        <li><a href="#infos" @click="closeMobileMenu">Infos Pratiques</a></li>
        <li><a href="#lineup" @click="closeMobileMenu">Line-up</a></li>
      </ul>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const scrolled = ref(false);
const mobileMenuOpen = ref(false);
const logoTitle = ref(null);
const logoContainer = ref(null);

// Gestion du menu mobile
const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;
  if (mobileMenuOpen.value) {
    document.body.style.overflow = 'hidden';
  } else {
    document.body.style.overflow = '';
  }
};

const closeMobileMenu = () => {
  mobileMenuOpen.value = false;
  document.body.style.overflow = '';
};

// Gestion du changement d'apparence du header au scroll
const handleScroll = () => {
  if (window.scrollY > 50) {
    scrolled.value = true;
  } else {
    scrolled.value = false;
  }
};

// Fonction pour ajuster la taille de la police du titre
const adjustLogoFontSize = () => {
  if (!logoTitle.value || !logoContainer.value) return;
  
  const containerWidth = logoContainer.value.clientWidth;
  const title = logoTitle.value;
  
  // Réinitialiser la taille de police pour mesurer correctement
  title.style.fontSize = '2rem';
  
  // Vérifier si le titre déborde et ajuster la taille
  if (title.scrollWidth > containerWidth) {
    const ratio = containerWidth / title.scrollWidth;
    const newSize = Math.max(1, Math.floor(2 * ratio * 100) / 100);
    title.style.fontSize = `${newSize}rem`;
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  
  // Observer les changements de taille pour ajuster la police
  if (typeof ResizeObserver !== 'undefined') {
    const resizeObserver = new ResizeObserver(() => {
      adjustLogoFontSize();
    });
    
    if (logoContainer.value) {
      resizeObserver.observe(logoContainer.value);
    }
  }
  
  // Ajuster immédiatement la taille de police
  adjustLogoFontSize();
  
  // Ajuster après le chargement complet
  window.addEventListener('load', adjustLogoFontSize);
  
  // Ajuster lors des modifications de fenêtre
  window.addEventListener('resize', adjustLogoFontSize);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  window.removeEventListener('load', adjustLogoFontSize);
  window.removeEventListener('resize', adjustLogoFontSize);
});
</script>

<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 20px 0;
  z-index: 1000;
  transition: all 0.3s ease;
  background-color: transparent;
}

.header-scrolled {
  background-color: var(--purple-deep);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
  padding: 10px 0;
}

.container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo h1 {
  font-size: 2rem;
  margin: 0;
  background: linear-gradient(to right, var(--orange-primary), var(--orange-quinary));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 700;
  letter-spacing: 1px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.desktop-nav ul {
  display: flex;
  list-style: none;
  gap: 30px;
}

.desktop-nav a {
  color: white;
  font-weight: 500;
  position: relative;
  padding: 5px 0;
}

.desktop-nav a::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--orange-primary);
  transition: width 0.3s ease;
}

.desktop-nav a:hover::after {
  width: 100%;
}

.mobile-menu-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
}

.bar {
  width: 30px;
  height: 3px;
  background-color: white;
  border-radius: 5px;
  transition: all 0.3s ease;
}

.bar.animate:nth-child(1) {
  transform: translateY(8px) rotate(45deg);
}

.bar.animate:nth-child(2) {
  opacity: 0;
}

.bar.animate:nth-child(3) {
  transform: translateY(-8px) rotate(-45deg);
}

.mobile-menu {
  position: fixed;
  top: 70px;
  right: -100%;
  width: 100%;
  height: calc(100vh - 70px);
  background-color: var(--purple-deep);
  transition: right 0.3s ease;
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
}

.mobile-menu.open {
  right: 0;
}

.mobile-menu ul {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 0;
  text-align: center;
}

.mobile-menu a {
  color: white;
  font-size: 24px;
  font-weight: 500;
  padding: 10px;
  display: block;
}

@media (max-width: 768px) {
  .desktop-nav {
    display: none;
  }
  
  .mobile-menu-toggle {
    display: flex;
  }
  
  .logo h1 {
    font-size: 1.5rem;
  }
}

@media (max-width: 480px) {
  .logo h1 {
    font-size: 1.2rem;
  }
}

@media (max-width: 360px) {
  .logo h1 {
    font-size: 1rem;
  }
}
</style>
