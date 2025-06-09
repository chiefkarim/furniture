<script setup lang="ts">
import { ref } from "vue";
import ArrowIcon from "~/assets/icons/scroll-down.svg";

// Variable réactive pour savoir si le menu est ouvert (true) ou fermé (false)
const isMenuOpen = ref(false);
</script>
<template>
  <div class="container-wrapper">
    <header class="container app-header">
      <div class="header-content-wrapper">
        <div class="hero-section">
          <div class="hero-left">
            <!-- Top Navigation Bar -->
            <div class="top-nav">
              <div class="logo">antic</div>

              <!-- Bouton menu mobile (image instead of SVG) -->
              <button
                class="menu-toggle"
                @click="isMenuOpen = !isMenuOpen"
                aria-label="Basculer le menu"
              >
                <img src="/images/menu.svg" alt="menu bar" />
              </button>

              <!-- Navigation principale -->
              <nav class="main-nav" :class="{ open: isMenuOpen }">
                <ul>
                  <li><NuxtLink to="/products">Products</NuxtLink></li>
                  <li><NuxtLink to="/rooms">Rooms</NuxtLink></li>
                  <li><NuxtLink to="/services">Services</NuxtLink></li>
                  <li><NuxtLink to="/inspirations">Inspirations</NuxtLink></li>
                </ul>
              </nav>
            </div>

            <!-- Contenu principal (h1, description, etc.) -->
            <div class="header-main-content">
              <p class="tagline">HOME DESIGN</p>
              <h1>
                Elegance for<br />
                Interiors &<br />
                Exteriors
              </h1>
              <p class="description">
                We provide everyone with modern,<br />
                trendy, quality furniture
              </p>
              <a href="#rooms" class="scroll-indicator">
                <ArrowIcon />
              </a>
            </div>
          </div>

          <div class="hero-right">
            <!-- L’image de fond viendra ici -->
          </div>
        </div>
      </div>

      <!-- Icône de chat -->
      <button class="chat-icon">
        <img src="/images/contact.svg" />
      </button>
    </header>
  </div>
</template>

<style>
.container {
  max-width: 1444px;
  margin: 0 auto 0 auto;
  padding: 0 clamp(1rem, 5vw, 6.5rem);
  overflow-x: visible;
}
.container-wrapper {
  height: 100vh;
}

.app-header {
  min-height: 100vh;
  display: flex;
  font-family: var(--font-sans);
}
.header-content-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
}
.header-main-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100%;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
.hero-section {
  display: flex;
  flex-grow: 1;
  width: 100%;
}
.hero-left {
  flex-basis: 40%;
  padding: 35px 0 0%;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  min-height: 100%;
}
.top-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-top: 25px;
  position: relative; /* pour que le menu en absolute se réfère à cette zone */
}
.logo {
  font-family: var(--font-serif);
  font-weight: 700;
  font-size: 34px;
  color: var(--text-primary);
  cursor: pointer;
}
/* Bouton menu (mobile) */
.menu-toggle {
  display: none;
  background: transparent;
  border: none;
  cursor: pointer;
  color: var(--text-secondary);
}
.main-nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
}
.main-nav li:not(:first-child) {
  margin-left: 24px;
}
.main-nav li:first-child {
  margin-left: 32px;
}
.main-nav a {
  text-decoration: none;
  color: var(--text-secondary);
  font-size: 18px;
  font-weight: 400;
  transition: color 0.3s ease;
  letter-spacing: 0;
  line-height: 25px;
}
.main-nav a:hover {
  color: #8c5046;
}
.tagline {
  font-family: var(--font-sans);
  font-size: 14px;
  color: var(--text-primary);
  text-transform: uppercase;
  margin-bottom: 50px;
  line-height: 20px;
  letter-spacing: 1px;
  font-weight: 700;
}
.hero-left h1 {
  font-family: var(--font-serif);
  font-size: 50px;
  color: var(--text-primary);
  line-height: 70px;
  margin-bottom: 30px;
  font-weight: 300;
  letter-spacing: -0.4px;
}
.description {
  font-family: var(--font-sans);
  font-size: 22px;
  color: var(--brown-light);
  line-height: 30.8px;
  font-weight: 400;
  margin-bottom: 48px;
  letter-spacing: 0;
}
.scroll-indicator svg {
  width: 50px;
  height: 50px;
  color: transparent;
  display: flex;
  stroke: var(--text-primary);
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.hero-right {
  background-image: url(/images/lights.jpg);
  background-size: cover;
  background-position: center;
  position: absolute;
  right: 0;
  width: 50vw;
  height: 100vh;
}

.chat-icon {
  position: absolute;
  top: 50px;
  right: 50px;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  z-index: 20;
}

.chat-icon img {
  width: 50px;
  height: 50px;
}

@media (max-width: 1030px) {
  .app-header {
    height: 100vh;
  }
  .hero-right {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    z-index: 1;
    background-color: #70645833;
  }
  .header-main-content {
    align-items: center;
  }
  .hero-left {
    z-index: 2;
    position: relative;
    align-items: center;
    text-align: center;
  }
  .logo {
    color: white;
    font-size: 34px;
  }
  .tagline {
    color: white;
    letter-spacing: 1px;
    line-height: 20px;
    font-size: 14px;
    font-family: var(--font-sans);
  }

  .scroll-indicator svg {
    stroke: white;
  }
  .hero-left h1 {
    color: white;
    line-height: 40px;
    font-size: 35px;
    font-weight: 400;
    letter-spacing: -0.3px;
  }
  .chat-icon {
    display: none;
  }

  /* --- Vue mobile (<=768px) --- */
  .app-header {
    min-height: auto;
  }
  .hero-section {
    flex-direction: column;
  }
  .hero-left {
    flex-basis: auto;
    width: 100%;
    order: 2;
    justify-content: flex-start;
  }
  .top-nav {
    margin-bottom: 30px;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    position: relative; /* Pour que le menu positionné en absolute se base sur ce parent */
  }

  /* Afficher le bouton menu */
  .menu-toggle {
    display: block;
  }

  /* Positionner le menu en absolute et retirer la bordure */
  .main-nav {
    position: absolute;
    top: 100%; /* Juste sous .top-nav */
    left: 0;
    width: 100%;
    background-color: var(--bg-main);
    max-height: 0;
    overflow: hidden;
    z-index: 50; /* Suffisamment élevé pour passer au-dessus du contenu */
    transition: max-height 0.3s ease;
    /* Suppression de la bordure horizontale */
    /* border-top: 1px solid var(--light-border-color); */
  }
  /* Quand ‘open’, on déploie le menu par-dessus le contenu */
  .main-nav.open {
    max-height: 500px; /* Ajuster si nécessaire selon la hauteur des liens */
  }

  /* Mise en colonne des liens */
  .main-nav ul {
    flex-direction: column;
    align-items: flex-start;
    padding: 10px 0;
  }
  .main-nav li {
    margin: 10px 0;
    width: 100%;
  }
  .main-nav a {
    display: block;
    width: 100%;
    padding: 8px 15px;
    color: var(--text-secondary);
  }

  .hero-right {
    flex-basis: auto;
    width: 100%;
    min-height: 300px;
    order: 1;
  }

  .chat-icon {
    top: 20px;
    right: 20px;
    width: 40px;
    height: 40px;
  }
  .chat-icon svg {
    width: 18px;
    height: 18px;
  }

  /* --- Vue très petit écran (<=500px) --- */
  .app-header {
    height: 100vh;
  }
  .container-wrapper {
  }
  .hero-right {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
  }
  .hero-left {
    z-index: 2;
    position: relative;
    align-items: center;
    text-align: center;
  }
  .hero-left h1 {
    margin-bottom: 24px;
  }
  .logo {
    color: white;
    font-size: 34px;
  }
  .tagline {
    margin-bottom: 24px;
  }

  .description {
    color: white;
    font-weight: 400;
    font-size: 18px;
    list-style: 25px;
    margin-bottom: 24px;
  }
  .scroll-indicator {
    background-color: transparent;
  }

  .chat-icon {
    display: none;
  }
}
</style>
