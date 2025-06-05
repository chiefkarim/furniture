<template>
  <section class="container design-services-section">
    <div class="services-grid">
      <div class="main-title-column">
        <h1>
          We stay by your<br />
          side to design<br />
          your projects
        </h1>
        <a href="#" class="find-out-more-link">
          Find out more <span class="arrow">›</span>
        </a>
      </div>

      <div class="services-grid">
        <div class="service-item">
          <h3>Our Advices</h3>
          <p>
            What if you took advantage of this rather special period to rethink
            your interior? You spend more time at home so you might as well feel
            good there.
          </p>
        </div>

        <div class="service-item">
          <h3>Click and Collect</h3>
          <p>
            Adapted and contactless. Free from € 200 of purchases in stores
            offering the service.
          </p>
        </div>

        <div class="service-item">
          <h3>Conception Service</h3>
          <p>
            Personalized service with an expert advisor for your interior and
            exterior decoration or layout projects.
          </p>
        </div>

        <div class="service-item">
          <h3>Installation Service</h3>
          <p>
            Our furniture packaged in flat packs are designed for easy assembly.
            But you can call on our partner.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
// No specific script logic needed for this static example
</script>

<style scoped>
.design-services-section {
  background-color: var(
    --bg-main
  ); /* Assuming same background as other sections */
  padding: 70px 0; /* Adjust vertical padding */
  font-family: var(--font-sans);
}

.container {
  max-width: 1444px; /* ou ce que tu préfères */
  margin: 0 auto;
  position: relative;
  padding: 70px clamp(1rem, 5vw, 6.5rem);
}

.services-grid {
  display: grid;
  /* Define 3 columns: 1st wider for title, next 2 for services.
     Adjust fr units for desired proportions. e.g., 2fr 1fr 1fr means first column is twice as wide.
     Visually, the title column looks slightly less than half, and the other two are equal.
     Let's try: title ~40-45%, services ~27-30% each.
  */
  grid-template-columns: 1fr 1fr; /* Example: 1.5 + 1 + 1 = 3.5 parts. Title is 1.5/3.5 ~ 43% */
  gap: 40px; /* Gap between columns */
}

.main-title-column {
  display: flex;
  flex-direction: column;
}

.main-title-column h1 {
  font-family: var(--font-serif);
  font-size: 55px; /* Large title */
  color: var(--text-secondary); /* Title uses secondary text color in image */
  line-height: 60px;
  font-weight: 400; /* Design looks like a regular weight */
  font-weight: 400;
  letter-spacing: -0.6px;
  margin-bottom: 30px; /* Space below title before link */
}

.find-out-more-link {
  font-family: "Karla";
  font-size: 17px;
  color: var(--text-primary); /* Link uses primary color */
  text-decoration: none;
  font-weight: 700; /* Slightly bolder */
  display: inline-flex; /* To align arrow correctly */
  line-height: 25px;
  letter-spacing: 0.3px;
  align-items: center;
}

.find-out-more-link .arrow {
  margin-left: 8px;
  font-size: 20px;
}

.services-column {
  display: flex;
  flex-direction: column;
  gap: 50px; /* Space between service items within a column */
}

.service-item h3 {
  font-family: var(
    --font-sans
  ); /* Or --font-sans if preferred for these subheadings */
  font-size: 25px; /* Adjust size */
  line-height: 30px;
  letter-spacing: -0.2px;
  color: var(--text-primary); /* Service titles use primary color */
  margin-bottom: 15px;
  font-weight: 600; /* Bolder service titles */
}

.service-item p {
  font-family: var(--font-sans);
  font-size: 18px;
  line-height: 25px;
  font-weight: 400;
  color: var(--text-secondary); /* Service description uses secondary color */
  letter-spacing: 0;
  margin: 0;
}

@media (max-width: 992px) {
  /* Mobile */
  .design-services-section {
    padding: 48px clamp(1rem, 5vw, 6.5rem);
  }

  .services-grid {
    grid-template-columns: 1fr; /* Stack all columns */
    gap: 40px; /* Gap between stacked sections */
  }
  .main-title-column {
    font-size: 35px;
    letter-spacing: -0.3px;
  }
  .main-title-column h1 {
    font-size: 40px; /* Scale down */
    margin-bottom: 25px;
  }
  .find-out-more-link {
    margin-top: 0; /* Reset margin-top when stacked */
    font-size: 17px;
    font-weight: 900;
  }
  .services-column {
    gap: 30px; /* Reduce gap between service items when stacked */
    text-align: center; /* Center text in service items */
  }
  .service-item {
    margin-bottom: 10px; /* Small space between individual service items if columns stack */
  }
  .service-item h3 {
    font-size: 25px;
  }
  .service-item p {
    font-size: 18px;
  }
}
</style>
