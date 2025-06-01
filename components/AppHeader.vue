<template>
  <header class="app-header">
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
/* Consolidated Font Import */
@import url("https://fonts.googleapis.com/css2?family=Merriweather:wght@700&family=Varta:wght@300;400&display=swap");

.app-header {
  --text-primary: #a06056;
  --text-secondary: #706458e5;
  --bg-left-column: #f3eee8;
  --icon-color: var(--text-primary);
  --icon-secondary-color: var(--text-secondary);

  min-height: 100vh;
  display: flex; /* Changed from flex to allow hero-section to be the main flex container */
  position: relative;
  font-family: "Varta", sans-serif;
  /* Background color removed from app-header, will be on hero-left */
}

.header-content-wrapper {
  width: 100%;
  display: flex; /* This will make hero-section grow */
  flex-direction: column; /* This ensures hero-section can take height */
}

/* Hero Section is the main flex container for left and right columns */
.hero-section {
  display: flex;
  flex-grow: 1; /* Allows hero-section to take available space in header-content-wrapper */
  width: 100%;
}

.hero-left {
  flex-basis: 40%;
  background-color: var(--bg-left-column); /* Background now on hero-left */
  padding: 35px 7% 50px 7%; /* Consistent padding for the whole left block */
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Pushes top-nav to top, scroll-indicator to bottom */
  box-sizing: border-box;
  min-height: 100%; /* Ensure it tries to take full height of its parent */
}

/* Top Navigation is now a static block inside hero-left */
.top-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%; /* Takes full width of hero-left's content area */
  margin-bottom: 40px; /* Space between nav and main content, adjust as needed */
  margin-top: 25px; /* Space between nav and main content, adjust as needed */
}

.logo {
  font-family: "Merriweather", serif;
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
  margin-left: 40px; /* Adjusted for visual balance */
}

.main-nav a {
  text-decoration: none;
  color: var(--text-primary);
  font-family: "Varta", sans-serif;
  font-size: 15px;
  font-weight: 400;
  transition: color 0.3s ease;
}

.main-nav a:hover {
  color: #8c5046;
}

/* This div wraps the main text content to allow space-between in hero-left */
.hero-left-main-content {
  /* No specific styles needed if just for grouping */
  flex-grow: 1; /* Allows this section to push the scroll indicator down if needed */
  display: flex;
  flex-direction: column;
  justify-content: center; /* Vertically center this block of text if desired */
}

.tagline {
  font-family: "Merriweather", serif;
  font-size: 11px;
  color: var(--text-primary);
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 25px;
  font-weight: 700;
}

.hero-left h1 {
  font-family: "Merriweather", serif;
  font-size: 56px;
  color: var(--text-primary);
  line-height: 1.25;
  margin-bottom: 30px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.description {
  font-family: "Varta", sans-serif;
  font-size: 16px;
  color: var(--text-secondary);
  line-height: 1.7;
  /* margin-bottom removed as scroll-indicator-wrapper will handle bottom spacing */
  font-weight: 300;
}

.scroll-indicator-wrapper {
  /* Wrapper to help with positioning if needed, or just direct styling for scroll-indicator */
  display: flex;
  /* justify-content: flex-start; /* Aligns to the left by default */
  margin-top: 50px; /* Space above scroll indicator */
}

.scroll-indicator {
  width: 44px;
  height: 44px;
  border: 1.5px solid var(--icon-color);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--icon-color);
  cursor: pointer;
  transition:
    background-color 0.3s ease,
    border-color 0.3s ease;
}

.scroll-indicator svg {
  width: 20px;
  height: 20px;
}

.scroll-indicator:hover {
  background-color: rgba(160, 96, 86, 0.05);
  border-color: #8c5046;
}

.hero-right {
  flex-basis: 60%;
  background-image: url("/images/lights.jpg");
  background-size: cover;
  background-position: center;
  /* min-height: 100vh; This ensures the image part tries to be full height */
  /* No specific min-height needed if .hero-section and its parents handle height distribution */
  box-sizing: border-box;
}

/* Chat Icon Styling */
.chat-icon {
  position: absolute;
  top: 35px; /* Vertical alignment with top content of hero-left */
  /* Position it based on the right edge of the viewport */
  right: 3.5%; /* If hero-right is 60% and we want it ~center of that 60% from right edge of viewport */
  /* Or more precisely: right: calc( (60% / 2) - (44px / 2) - (7% * 0.6) ); /* This is getting complex, better to use a simpler percentage */
  /* Let's try a value that visually puts it in the right half: */
  /* right: 7%; */ /* This was for the whole page. For right half, needs smaller % if from viewport edge */
  /* The easiest for exact placement in the right half is to position from the left edge of the image */
  /* However, since it's relative to app-header, we can use right padding value */
  right: 7%; /* This should match the left column's right edge, visually placing it at start of image area. Adjust as needed. */
  /* To place it correctly in the image area: */
  /* If hero-left is 40%, then hero-right starts at 40% from left.
     If we want it, say, 7% from the right edge of the *viewport*: */
  /* right: 7%; */

  width: 44px;
  height: 44px;
  background-color: #fff;
  border: 1px solid #eaeaea;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  color: var(--icon-secondary-color);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  z-index: 20;
  padding: 0;
}
.chat-icon:hover {
  background-color: #f7f7f7;
  border-color: #e0e0e0;
}

.chat-icon svg {
  width: 20px;
  height: 20px;
}

/* --- Responsive Adjustments --- */
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
  .hero-left {
    flex-basis: 50%; /* Give text more space on medium screens */
    padding: 30px 5% 40px 5%;
  }
  .hero-right {
    flex-basis: 50%;
  }
  .logo {
    font-size: 28px;
  }
  .main-nav li {
    margin-left: 25px;
  }
  .main-nav a {
    font-size: 14px;
  }
  .hero-left h1 {
    font-size: 40px;
  }
  .description {
    font-size: 15px;
  }
  .chat-icon {
    right: 5%;
    top: 30px;
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
    order: 2; /* Text below image */
    padding: 30px 7% 40px 7%;
    justify-content: flex-start; /* Align content to top on mobile */
  }
  .top-nav {
    margin-bottom: 30px;
    /* On mobile, maybe center logo and hide nav, or stack them */
    flex-direction: column; /* Example: stack logo and nav */
    align-items: flex-start; /* Align items to left when stacked */
  }
  .logo {
    margin-bottom: 15px; /* Space if nav is below */
  }
  .main-nav {
    width: 100%; /* If stacked */
  }
  .main-nav ul {
    flex-direction: column; /* Stack nav items */
    align-items: flex-start;
    width: 100%;
  }
  .main-nav li {
    margin-left: 0;
    margin-bottom: 10px; /* Space between stacked nav items */
    width: 100%;
  }
  .main-nav a {
    width: 100%;
    display: block; /* Make links full width */
  }

  .hero-left-main-content {
    /* On mobile, text can be centered */
    align-items: center;
    text-align: center;
  }
  .scroll-indicator-wrapper {
    justify-content: center; /* Center scroll indicator on mobile */
    margin-top: 40px;
  }

  .hero-right {
    flex-basis: auto;
    width: 100%;
    min-height: 300px;
    order: 1; /* Image above text */
  }

  .hero-left h1 {
    font-size: 36px;
  }
  .description {
    font-size: 16px;
  }

  .chat-icon {
    /* Adjust chat icon for mobile, maybe top right of viewport */
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
</style>
