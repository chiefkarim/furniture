<template>
  <section class="design-services-section">
    <div class="container">
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

        <div class="services-column">
          <div class="service-item">
            <h3>Our Advices</h3>
            <p>
              What if you took advantage of this rather special period to
              rethink your interior? You spend more time at home so you might as
              well feel good there.
            </p>
          </div>
          <div class="service-item">
            <h3>Conception Service</h3>
            <p>
              Personalized service with an expert advisor for your interior and
              exterior decoration or layout projects.
            </p>
          </div>
        </div>

        <div class="services-column">
          <div class="service-item">
            <h3>Click and Collect</h3>
            <p>
              Adapted and contactless. Free from € 200 of purchases in stores
              offering the service.
            </p>
          </div>
          <div class="service-item">
            <h3>Installation Service</h3>
            <p>
              Our furniture packaged in flat packs are designed for easy
              assembly. But you can call on our partner.
            </p>
          </div>
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
  padding: 100px 0; /* Adjust vertical padding */
  font-family: var(--font-sans);
}

.container {
  max-width: var(--page-max-width, 1280px); /* Use global max-width */
  margin: 0 auto;
  padding: 0 4%; /* Consistent horizontal padding with other sections */
  box-sizing: border-box;
}

.services-grid {
  display: grid;
  /* Define 3 columns: 1st wider for title, next 2 for services.
     Adjust fr units for desired proportions. e.g., 2fr 1fr 1fr means first column is twice as wide.
     Visually, the title column looks slightly less than half, and the other two are equal.
     Let's try: title ~40-45%, services ~27-30% each.
  */
  grid-template-columns: 1.5fr 1fr 1fr; /* Example: 1.5 + 1 + 1 = 3.5 parts. Title is 1.5/3.5 ~ 43% */
  gap: 40px; /* Gap between columns */
}

.main-title-column {
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Pushes title up and link down if there's enough height */
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
  margin-top: auto; /* Pushes link to bottom if column has extra space */
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
    --font-serif
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

/* --- Responsive Adjustments --- */
@media (max-width: 1024px) {
  /* Tablet */
  .services-grid {
    grid-template-columns: 1.8fr 1fr 1fr; /* Give title slightly more relative space */
    gap: 30px;
  }
  .main-title-column h1 {
    font-size: 52px;
  }
  .service-item h3 {
    font-size: 20px;
  }
  .service-item p {
    font-size: 14px;
  }
  .find-out-more-link {
    font-size: 15px;
  }
}

@media (max-width: 768px) {
  /* Mobile */
  .design-services-section {
    padding: 60px 0 70px 0;
  }
  .container {
    padding: 0 5%; /* Standard mobile padding */
  }
  .services-grid {
    grid-template-columns: 1fr; /* Stack all columns */
    gap: 40px; /* Gap between stacked sections */
  }
  .main-title-column {
    align-items: center; /* Center content in the title column */
    text-align: center;
  }
  .main-title-column h1 {
    font-size: 40px; /* Scale down */
    margin-bottom: 25px;
  }
  .find-out-more-link {
    margin-top: 0; /* Reset margin-top when stacked */
    font-size: 16px;
  }
  .services-column {
    gap: 30px; /* Reduce gap between service items when stacked */
    text-align: center; /* Center text in service items */
  }
  .service-item {
    margin-bottom: 10px; /* Small space between individual service items if columns stack */
  }
  .service-item h3 {
    font-size: 20px;
  }
  .service-item p {
    font-size: 14px;
  }
}
</style>
