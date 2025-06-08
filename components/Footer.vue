<template>
  <footer class="app-footer">
    <div class="container">
      <div class="footer-main-content">
        <div class="footer-column logo-column">
          <div class="footer-logo">antic</div>
        </div>
        <div class="footer-column links-column">
          <h4>About</h4>
          <ul>
            <li><a href="#">Our story</a></li>
            <li><a href="#">Our stores</a></li>
            <li><a href="#">Our partners</a></li>
          </ul>
        </div>

        <div class="footer-column links-column">
          <h4>Services</h4>
          <ul>
            <li><a href="#">Click and collect</a></li>
            <li><a href="#">Conception</a></li>
            <li><a href="#">Installation</a></li>
            <li><a href="#">Advices</a></li>
            <li><a href="#">Gift card</a></li>
          </ul>
        </div>

        <div class="footer-column links-column">
          <h4>Products</h4>
          <ul>
            <li><a href="#">Furniture</a></li>
            <li><a href="#">Decoration</a></li>
            <li><a href="#">Storage</a></li>
            <li><a href="#">Baby and child</a></li>
            <li><a href="#">Connected home</a></li>
          </ul>
        </div>

        <div class="footer-column links-column">
          <h4>Rooms</h4>
          <ul>
            <li><a href="#">Living room</a></li>
            <li><a href="#">Dining room</a></li>
            <li><a href="#">Cooked</a></li>
            <li><a href="#">Bedroom</a></li>
            <li><a href="#">Bathroom</a></li>
            <li><a href="#">Office</a></li>
            <li><a href="#">Laundry</a></li>
            <li><a href="#">Garage</a></li>
          </ul>
        </div>

        <div class="footer-column planet-column">
          <h4>We respect our planet</h4>
          <img
            src="/images/footer.jpg"
            alt="Respecting our planet"
            class="planet-image"
          />
          <p>
            We’re taking positive steps to reduce our impact on the planet. For
            us, that means retailing responsibly. We’ve set a number of goals to
            get us there.
          </p>
          <a href="#" class="learn-more-footer"
            >Learn more <span class="arrow">›</span></a
          >
        </div>
      </div>

      <!-- Social Media Icons -->
      <div class="footer-social-media">
        <a href="#" aria-label="Facebook" class="social-icon">
          <!-- Placeholder: Replace with actual SVG -->

          <img src="/images/facebook.svg" />
        </a>
        <a href="#" aria-label="Twitter" class="social-icon">
          <img src="/images/twitter.svg" />
        </a>
        <a href="#" aria-label="LinkedIn" class="social-icon">
          <!-- Placeholder: Replace with actual SVG -->

          <img src="/images/linkedin.svg" />
        </a>
        <a href="#" aria-label="Instagram" class="social-icon">
          <!-- Placeholder: Replace with actual SVG -->
          <img src="/images/instagram.svg" />
        </a>
      </div>

      <!-- Bottom Bar -->
      <div class="footer-bottom-bar">
        <span class="copyright">© 2021 Agence Dnd</span>
        <nav class="utility-links">
          <a href="#">Privacy policy</a>
          <a href="#">Term of service</a>
          <a href="#">Language</a>
        </nav>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
// No script logic needed for this static example
</script>

<style scoped>
.app-footer {
  background-color: var(--bg-main);
  color: var(--text-secondary);
  padding: 60px 0 30px 0; /* Top padding, then less bottom padding */
  font-family: var(--font-sans);
  font-size: 14px; /* Default font size for footer text */
  line-height: 1.6;
}
.container {
  max-width: 1444px;
  padding: 0 clamp(1rem, 5vw, 6.5rem);
}
.footer-main-content {
  display: grid;
  /* 1 for logo, 4 for links, 1.5 for planet. Adjust fr units for proportions. */
  grid-template-columns: 1fr repeat(4, 0.8fr) 1.5fr;
  gap: 48px; /* Gap between columns */
  margin-bottom: 48px; /* Space before social icons */
  padding-bottom: 40px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.05); /* Very subtle separator */
}

.footer-column h4 {
  font-family: var(--font-sans);
  font-size: 25px;
  color: var(
    --brown-dark
  ); /* Using secondary for headings in footer to be less prominent */
  font-weight: 600; /* Bolder headings */
  margin-bottom: 22px;
  line-height: 30px;
  letter-spacing: -0.2px;
}
.footer-main-content .footer-column:first-child {
  margin-right: 44px;
}

.footer-logo {
  font-family: var(--font-serif); /* Matches header logo */
  font-size: 34px; /* Matches header logo */
  font-weight: 700;
  color: var(--brown-dark); /* Logo in footer is secondary color */
  line-height: 25px;
  letter-spacing: 2px; /* Slightly less than header if needed */
}

.links-column ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.links-column li {
  margin-bottom: 10px;
}

.links-column a {
  color: var(--text-secondary);
  text-decoration: none;
  font-size: 18px;
  line-height: 25px;
  font-weight: 400;
  letter-spacing: 0;
}

.links-column a:hover {
  color: var(--text-primary); /* Primary color on hover for links */
  text-decoration: underline;
}

.planet-column p {
  font-size: 16px;
  line-height: 25px;
  font-family: var(--font-sans);
  letter-spacing: 0;
  font-family: "Varta";
  font-weight: 400;
  margin-bottom: 15px;
}

.planet-image {
  width: 100%;
  max-width: 250px; /* Limit image size */
  height: 182px;
  object-fit: cover;
  margin-bottom: 15px;
}

.learn-more-footer {
  font-family: "Karla"; /* Or Karla */
  font-size: 17px;
  line-height: 25px;
  color: var(--text-primary);
  text-decoration: none;
  font-weight: 500;
  display: inline-flex;
  align-items: center;
  letter-spacing: 0.3px;
}
.learn-more-footer .arrow {
  margin-left: 6px;
  font-size: 16px;
}

.footer-social-media {
  display: flex;
  justify-content: center; /* Center social icons */
  align-items: center;
  margin-bottom: 20px; /* Space before bottom bar */
}

.social-icon {
  color: var(--text-secondary); /* Icon color */
  margin: 0 10px; /* Spacing between icons */
  display: inline-block; /* For proper spacing and hover */
  transition: color 0.3s ease;
}
.social-icon svg {
  display: block; /* Removes extra space below SVG if any */
}
.social-icon:hover {
  color: var(--text-primary); /* Primary color on hover */
}

.footer-bottom-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 18px; /* Smaller text for bottom bar */
  color: var(--text-secondary);
  opacity: 0.8; /* Slightly faded out */
  letter-spacing: 0;
  line-height: 25px;
  opacity: 0.7;
  font-weight: 400;
}
.utility-links a,
.copyright {
  text-decoration: none;
  color: #706458b2;
  display: inline-block; /* Ensure they space out */
  text-align: left;
  line-height: 25px;
  letter-spacing: 0;
  font-weight: 400;
}

.utility-links a {
  margin: 0 10px 0 0; /* Adjust spacing for utility links */
}

.utility-links a:hover {
  color: var(--text-primary);
  text-decoration: underline;
}

/* --- Responsive Adjustments --- */

@media (max-width: 992px) {
  /* Mobile */
  .app-footer {
    padding: 40px 0 20px 0;
  }

  .footer-main-content {
    grid-template-columns: 1fr; /* Stack all columns */
    text-align: left; /* Center text in stacked columns */
    gap: 40px;
    border-bottom: none; /* Remove border on mobile */
    padding-bottom: 0;
  }
  .footer-column {
    margin-bottom: 20px; /* Add space between stacked sections */
  }
  .footer-column h4 {
    color: #121212;
    text-transform: capitalize;
  }
  .footer-column a {
    font-size: 18px;
    line-height: 25px;
    letter-spacing: -0.2px;
  }

  .logo-column {
    margin-bottom: 10px;
    align-self: center;
    text-align: center;
  }

  .links-column:nth-of-type(n) {
    /* Reset grid placement for stacking */
    grid-column: auto;
    margin-top: 0;
  }

  .footer-social-media {
    margin: 40px 0;
  }
  .social-icon {
    margin: 0 8px;
  }
  .footer-bottom-bar {
    flex-direction: column; /* Stack copyright and utility links */
    text-align: left;
    gap: 10px; /* Space between stacked items */
    padding-top: 20px;
    border-top: 1px solid rgba(0, 0, 0, 0.05);
    align-items: flex-start;
  }
  .planet-image {
    min-width: 100%;
    max-width: none;
    height: 192px;
  }
  .footer-main-content {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
