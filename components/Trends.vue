<template>
  <section class="latest-trends-section">
    <div class="container">
      <div class="trends-subscription">
        <div class="trends-info">
          <h2>Be aware of the latest trends</h2>
          <p>Stay informed of new trends, but also of our various offers.</p>
          <a href="#" class="learn-more-link"
            >Learn more <span class="arrow">›</span></a
          >
        </div>
        <form class="subscription-form" @submit.prevent="handleSubscription">
          <input
            type="email"
            v-model="email"
            placeholder="email@address.com"
            required
          />
          <button type="submit">Subscribe</button>
        </form>
      </div>

      <div class="inspirations-showcase">
        <div class="inspiration-images">
          <div
            v-for="(image, index) in inspirationImages"
            :key="index"
            class="inspiration-image-wrapper"
          >
            <div class="inspiration-image-card">
              <img :src="image.src" :alt="image.alt" />
            </div>

            <p class="inspiration-name">{{ image.name }}</p>
          </div>
        </div>

        <div class="inspiration-text-content">
          <h2 class="inspirations-title">Inspirations</h2>
          <p class="inspirations-description">
            Our experts are keen to stay on top of trends in order to offer you
            new inspirations for your interior and exterior every day. Remember
            that to inspire you we have to inspire ourselves and we want to
            share that with you.
          </p>
          <div class="pagination-wrapper">
            <div class="inspiration-pagination">
              <button
                class="nav-arrow prev-arrow"
                aria-label="Previous inspiration"
              >
                ‹
              </button>
              <button
                class="nav-arrow next-arrow"
                aria-label="Next inspiration"
              >
                ›
              </button>
            </div>

            <span class="page-info">01 / 05</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";

const email = ref("");

const inspirationImages = ref([
  {
    name: "chair",
    src: "/images/trend-1.png",
    alt: "Yellow chair inspiration",
  },
  {
    name: "cooked",
    src: "/images/trend-2.png",
    alt: "Kitchen inspiration with wicker lamp",
  },
  {
    name: "living room",
    src: "/images/trend-3.png",
    alt: "Living room sofa inspiration",
  },
  {
    name: "tables",
    src: "/images/trend-4.jpg",
    alt: "Living room sofa inspiration",
  },
]);

function handleSubscription() {
  if (email.value) {
    alert(`Subscribed with: ${email.value}`);
    // Here you would typically send the email to your backend
    email.value = ""; // Clear the input
  }
}
</script>

<style scoped>
.latest-trends-section {
  background-color: white;
  padding: 70px 0;
  font-family: var(--font-sans);
}

.container {
  max-width: 1280px;
  margin: 0 auto;
  position: relative;
} /* --- Trends Subscription Part --- */
.trends-subscription {
  padding-bottom: 60px; /* Optional: Space below subscription form before border */
  display: flex;
  /* border-bottom: 1px solid var(--light-border-color); /* Optional: if there's a subtle separator */
}

.trends-info {
  flex-basis: 55%; /* Adjust as needed */
}

.trends-info h2 {
  font-family: var(--font-serif);
  font-size: 35px; /* Adjust size */
  color: #121212; /* Matches "Find your room" title color */
  line-height: 40px;
  font-weight: 400;
  margin-bottom: 15px;
  text-align: left;
  letter-spacing: -0.3px;
}

.trends-info p {
  font-size: 18px;
  color: #706458e5;
  font-weight: 400;
  line-height: 25px;
  margin-bottom: 20px;
  letter-spacing: 0;
  max-width: 450px; /* Limit width of this text */
}

.learn-more-link {
  font-family: "Karla"; /* Or Karla if used consistently for these links */
  font-size: 17px;
  color: var(--text-primary);
  text-decoration: none;
  font-weight: 700;
  line-height: 25px;
  letter-spacing: -0.3px;
  display: inline-flex;
  align-items: center;
}

.learn-more-link .arrow {
  margin-left: 8px;
  font-size: 18px;
}

.subscription-form {
  margin-top: 10px; /* Align better with title if text wraps */
}

.subscription-form input[type="email"] {
  flex-grow: 1;
  padding: 12px 15px;
  border: 1px solid var(--light-border-color, #ddd); /* Use global or fallback */
  border-right: none; /* Button will form the right border */
  font-family: var(--font-sans);
  font-size: 14px;
  background-color: #f3eee84d; /* White background for input */
  color: var(--text-secondary);
  border-radius: 0; /* Sharp corners if desired */
  outline: none;
}
.subscription-form input[type="email"]::placeholder {
  color: #aaa; /* Lighter placeholder text */
}

.subscription-form button[type="submit"] {
  padding: 12px 25px;
  background-color: #534b42; /* Dark button like image */
  color: var(--white);
  border: 1px solid var(--text-secondary); /* Match background */
  cursor: pointer;
  font-family: "Karla";
  font-size: 14px;
  font-weight: 500;
  border-radius: 0;
  white-space: nowrap;
  transition: background-color 0.3s ease;
}

.subscription-form button[type="submit"]:hover {
  background-color: #50483e; /* Slightly darker shade for hover */
}

/* --- Inspirations Part --- */
.inspirations-showcase {
  /* No specific flex/grid here yet, default block layout */
}

.inspiration-images {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Three equal columns */
  gap: 25px; /* Gap between images */
  margin-bottom: 50px; /* Space below images before text */
}

.inspiration-image-card {
  aspect-ratio: 3 / 4; /* Portrait aspect ratio for images */
  overflow: hidden;
}

.inspiration-image-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.inspiration-text-content {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr; /* Title wider, description/pagination narrower */
  gap: 40px; /* Gap between title column and description/pagination column */
  align-items: flex-start; /* Align tops of items in grid */
}

.inspirations-title {
  font-family: var(--font-serif);
  font-size: 45px; /* Large title */
  color: var(--text-secondary);
  line-height: 40px;
  letter-spacing: -0.3px;
  font-weight: 300;
  /* text-align: right; /* If you want to align it to the right of its column */
}

.inspirations-description {
  font-size: 18px;
  line-height: 25px;
  color: var(--text-secondary);
  font-family: var(--font-sans);
  font-weight: 400;
  letter-spacing: 0;
  margin: 0;
}

.inspiration-pagination {
  display: flex;
  align-items: center;
  justify-content: flex-start; /* Align pagination to the right */
  margin-bottom: 20px;
}

.nav-arrow {
  background-color: transparent;
  border: 1.5px solid var(--text-primary);
  color: var(--text-primary);
  border-radius: 50%;
  width: 36px;
  height: 36px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  line-height: 1;
  cursor: pointer;
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}
.nav-arrow:hover {
  background-color: var(--text-primary);
  color: var(--white);
}
.nav-arrow.prev-arrow {
  margin-right: 11px;
}

.inspiration-pagination .page-info {
  font-size: 14px;
  color: var(--text-secondary);
  opacity: 0.7; /* Slightly less prominent */
}
.inspiration-name {
  display: none;
}
/* --- Responsive Adjustments --- */
@media (max-width: 992px) {
  /* Tablet */
  .trends-subscription {
    flex-direction: column; /* Stack info and form */
    gap: 30px;
    margin-bottom: 60px;
  }
  .trends-info {
    flex-basis: auto; /* Full width when stacked */
  }
  .trends-info p {
    max-width: none; /* Allow full width */
  }
  .subscription-form {
    display: flex;
    flex-direction: column;
    flex-basis: 100%;
    width: 320px;
  }

  .trends-info h2 {
    font-size: 32px;
  }

  .inspiration-images {
    grid-template-columns: repeat(2, 1fr); /* Three equal columns */
    /* Responsive grid */
    gap: 20px;
  }
  .inspiration-text-content {
    grid-template-columns: 1fr; /* Stack title and description/pagination */
    text-align: center; /* Center text */
    gap: 25px;
  }
  .inspirations-title {
    font-size: 40px;
    text-align: center; /* Ensure title is centered */
  }
  .inspiration-pagination {
    justify-content: center; /* Center pagination */
  }
  .inspiration-name {
    display: block;
    text-transform: capitalize;
  }
}

@media (max-width: 768px) {
  /* Mobile */
  .container {
    padding: 48px 7%;
  }
  .latest-trends-section {
    padding: 50px 0;
  }
  .trends-subscription {
    margin-bottom: 50px;
  }
  .trends-info h2 {
    font-size: 28px;
  }
  .trends-info p {
    font-size: 14px;
  }
  .learn-more-link {
    font-size: 14px;
  }
  .subscription-form input[type="email"],
  .subscription-form button[type="submit"] {
    font-size: 13px;
    padding: 10px 15px;
  }
  .subscription-form button[type="submit"] {
    padding: 10px 20px;
  }
  .inspirations-showcase {
    display: flex;
    flex-direction: column;
    flex-flow: column-reverse;
  }

  .inspiration-images {
    /* Keep responsive grid, or force 1 or 2 columns */
    /* grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); */
    gap: 15px;
    margin-bottom: 30px;
  }
  .inspiration-image-card {
    aspect-ratio: 1; /* Square images on mobile for simplicity or adjust */
  }

  .inspirations-title {
    font-size: 32px;
  }
  .inspiration-text-content {
    margin-top: 64px;
    margin-bottom: 40px;
  }
  .inspirations-description {
    font-size: 14px;
  }
  .nav-arrow {
    width: 32px;
    height: 32px;
    font-size: 18px;
  }
  .pagination-wrapper {
    display: none;
  }
}
</style>
