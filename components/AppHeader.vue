<template>
  <header class="container app-header">
    <div class="header-content-wrapper">
      <div class="hero-section">
        <div class="hero-left">
          <!-- Top Navigation Bar -->
          <div class="top-nav">
            <div class="logo">antic</div>
            <nav class="main-nav">
              <ul>
                <li><NuxtLink to="/products">Products</NuxtLink></li>
                <li><NuxtLink to="/rooms">Rooms</NuxtLink></li>
                <li><NuxtLink to="/services">Services</NuxtLink></li>
                <li><NuxtLink to="/inspirations">Inspirations</NuxtLink></li>
              </ul>
            </nav>
          </div>

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
          <div class="scroll-indicator">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M19 9L12 16L5 9"
                stroke="currentColor"
                stroke-width="1.5"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
        </div>
        <div class="hero-right">
          <!-- The background image will cover this area -->
        </div>
      </div>
    </div>

    <!-- Chat Icon (Top Right) -->
    <button class="chat-icon">
      <svg
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M21 11.5C21 16.7467 16.7467 21 11.5 21C10.5359 21 9.60445 20.8544 8.72965 20.5827L3 22L4.41734 16.2703C3.14563 14.3956 3 12.9641 3 11.5C3 6.25329 7.25329 2 11.5 2C16.7467 2 21 6.25329 21 11.5Z"
          stroke="currentColor"
          stroke-width="1.5"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>
  </header>
</template>

<script setup lang="ts">
// No specific script logic needed for this static example
</script>

<style>
.container {
  max-width: 1280px; /* ou ce que tu préfères */
  margin: 0 auto;
  position: relative;
}
.app-header {
  min-height: 100vh;
  display: flex;
  position: relative;
  font-family: var(--font-sans);
}

.header-content-wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
}

.hero-section {
  display: flex;
  flex-grow: 1;
  width: 100%;
}

.hero-left {
  flex-basis: 40%;
  background-color: var(--bg-main);
  padding: 35px 7% 50px 0%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-sizing: border-box;
  min-height: 100%;
}

.top-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  margin-bottom: 40px;
  margin-top: 25px;
}

.logo {
  font-family: var(--font-serif);
  font-weight: 700;
  font-size: 34px;
  line-height: 1.1;
  letter-spacing: 2px;
  color: var(--text-primary);
  cursor: pointer;
}

.main-nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
}

.main-nav li {
  margin-left: 40px;
}

.main-nav a {
  text-decoration: none;
  color: var(--text-secondary);
  font-family: var(--font-sans);
  font-size: 15px;
  font-weight: 400;
  transition: color 0.3s ease;
}

.main-nav a:hover {
  color: #8c5046;
}

.hero-left-main-content {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.tagline {
  font-family: var(--font-serif);
  font-size: 11px;
  color: var(--text-primary);
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 25px;
  font-weight: 700;
}

.hero-left h1 {
  font-family: var(--font-serif);
  font-size: 56px;
  color: var(--text-primary);
  line-height: 1.25;
  margin-bottom: 30px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.description {
  font-family: var(--font-sans);
  font-size: 16px;
  color: var(--text-secondary);
  line-height: 25px;
  letter-spacing: 0;
  font-weight: 300;
}

.scroll-indicator-wrapper {
  /* If you re-add this wrapper in HTML */
  display: flex;
  margin-top: 50px;
}

.scroll-indicator {
  width: 44px;
  height: 44px;
  border: 1.5px solid var(--icon-color-primary); /* Using global icon color variable */
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--icon-color-primary); /* Using global icon color variable */
  cursor: pointer;
  transition:
    background-color 0.3s ease,
    border-color 0.3s ease;
}

.scroll-indicator svg {
  width: 20px;
  height: 20px;
}
.scroll .scroll-indicator:hover {
  background-color: rgba(
    160,
    96,
    86,
    0.05
  ); /* Specific hover, or use var(--text-primary) with opacity */
  border-color: #8c5046; /* Specific hover, or create a --icon-color-primary-hover */
}

.hero-right {
  background-image: url(/images/lights.jpg);
  background-size: cover;
  background-position: center;
  margin-right: -196%;
  width: 53vw;
}

.chat-icon {
  position: absolute;
  top: 35px;
  right: 7%; /* Consider making this a CSS variable if used elsewhere or for consistency */
  width: 44px;
  height: 44px;
  background-color: var(--white); /* Using global white variable */
  border: 1px solid var(--light-border-color); /* Using global border color variable */
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: var(--icon-color-secondary); /* Using global icon color variable */
  box-shadow: 0 2px 8px var(--soft-shadow-color); /* Using global shadow variable */
  z-index: 20;
  padding: 0;
}
.chat-icon:hover {
  background-color: #f7f7f7; /* Specific hover, or make a --white-hover variable */
  border-color: #e0e0e0; /* Specific hover, or make a --light-border-color-hover */
}

.chat-icon svg {
  width: 20px;
  height: 20px;
}

/* --- Responsive Adjustments --- */
/* No changes needed here unless you want to use variables for breakpoints, which is advanced */
@media (max-width: 1200px) {
  .hero-left h1 {
    font-size: 48px;
  }
  .logo {
    font-size: 30px;
  }
  .main-nav li {
    margin-left: 35px;
  }
}

@media (max-width: 992px) {
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
  }
  .hero-left {
    z-index: 2;
    position: relative;
    background-color: #70645833;
    align-items: center;
    text-align: center;
  }

  .logo {
    color: white;
    font-size: 34px;
  }
  .tagline {
    color: white;
    letter-spacing: 1;
    line-height: 20px;
    font-size: 14px;
    font-family: var(--text-secondary);
  }
  .description {
    color: white;
    font-weight: 400;
    font-size: 18px;
  }
  .scroll-indicator {
    border-color: white;
    color: white;
    background-color: transparent;
  }

  .hero-left h1 {
    color: white;
    line-height: 40px;
    font-weight: 400;
    letter-spacing: -0.3px;
  }

  .chat-icon {
    display: none;
  }
}

@media (max-width: 768px) {
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
    padding: 30px 7% 40px 7%;
    justify-content: flex-start;
  }
  .top-nav {
    margin-bottom: 30px;
    flex-direction: column;
    align-items: flex-start;
  }
  .logo {
    margin-bottom: 15px;
  }
  .main-nav {
    width: 100%;
  }
  .main-nav ul {
    flex-direction: column;
    align-items: flex-start;
    width: 100%;
  }
  .main-nav li {
    margin-left: 0;
    margin-bottom: 10px;
    width: 100%;
  }
  .main-nav a {
    width: 100%;
    display: block;
  }

  .hero-left-main-content {
    /* If you re-add this wrapper */
    align-items: center;
    text-align: center;
  }
  .scroll-indicator-wrapper {
    /* If you re-add this wrapper */
    justify-content: center;
    margin-top: 40px;
  }

  .hero-right {
    flex-basis: auto;
    width: 100%;
    min-height: 300px;
    order: 1;
  }

  .hero-left h1 {
    font-size: 36px;
  }
  .description {
    font-size: 16px;
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
}

@media (max-width: 500px) {
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
  }
  .hero-left {
    z-index: 2;
    position: relative;
    background-color: #70645833;
    align-items: center;
    text-align: center;
  }

  .logo {
    color: white;
    font-size: 34px;
  }
  .tagline {
    color: white;
    letter-spacing: 1;
    line-height: 20px;
    font-size: 14px;
    font-family: var(--text-secondary);
  }
  .description {
    color: white;
    font-weight: 400;
    font-size: 18px;
  }
  .scroll-indicator {
    border-color: white;
    color: white;
    background-color: transparent;
  }

  .hero-left h1 {
    color: white;
    line-height: 40px;
    font-weight: 400;
    letter-spacing: -0.3px;
  }

  .chat-icon {
    display: none;
  }
}
</style>
