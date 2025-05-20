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
  </footer>
</template>

<script setup>
import { computed } from 'vue';

// Année courante pour le copyright
const currentYear = computed(() => new Date().getFullYear());

// Fonction pour remonter en haut de la page
const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  });
};
</script>

<style scoped>
.footer {
  background-color: var(--purple-deep);
  color: white;
  position: relative;
  padding: 120px 0 40px;
  margin-top: 80px;
}

.footer-wave {
  position: absolute;
  top: -70px;
  left: 0;
  width: 100%;
  overflow: hidden;
  line-height: 0;
  transform: rotate(180deg);
}

.footer-wave svg {
  position: relative;
  display: block;
  width: calc(100% + 1.3px);
  height: 70px;
}

.footer-wave .shape-fill {
  fill: var(--purple-deep);
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 30px;
  margin-bottom: 40px;
}

.footer-logo h2 {
  font-size: 2.5rem;
  margin: 0;
  background: linear-gradient(to right, var(--orange-primary), var(--orange-quinary));
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.tagline {
  margin-top: 5px;
  color: rgba(255, 255, 255, 0.7);
}

.footer-links h3,
.footer-socials h3 {
  font-size: 1.2rem;
  margin-bottom: 15px;
  color: white;
}

.footer-links ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 10px;
}

.footer-links a {
  color: rgba(255, 255, 255, 0.7);
  transition: color 0.3s ease;
  text-decoration: none;
}

.footer-links a:hover {
  color: var(--orange-primary);
  text-decoration: none;
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
  background: rgba(255, 255, 255, 0.1);
  color: white;
  transition: all 0.3s ease;
}

.social-icon:hover {
  background: var(--orange-primary);
  transform: translateY(-3px);
}

.social-icon svg {
  width: 18px;
  height: 18px;
}

.back-to-top {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: var(--orange-primary);
  color: white;
  position: absolute;
  right: 30px;
  bottom: 100px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.back-to-top:hover {
  background: var(--orange-quaternary);
  transform: translateY(-5px);
}

.back-to-top svg {
  width: 25px;
  height: 25px;
}

.copyright {
  text-align: center;
  margin-top: 30px;
  padding-top: 20px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.copyright p {
  margin: 5px 0;
  color: rgba(255, 255, 255, 0.6);
  font-size: 0.9rem;
}

.disclaimer {
  font-weight: 500;
  color: var(--orange-quaternary) !important;
}

@media (max-width: 768px) {
  .footer {
    padding: 100px 0 30px;
  }
  
  .footer-content {
    text-align: center;
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
