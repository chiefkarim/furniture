<template>
  <section class="find-room-section">
    <h2 class="section-title">Find your room</h2>

    <div class="room-showcase">
      <div class="showcase-info">
        <p class="info-text">
          Dining room, bedroom, bathroom or office. Find what you need
        </p>
      </div>

      <div class="room-cards-container">
        <div v-for="room in rooms" :key="room.name" class="room-card">
          <img :src="room.image" :alt="room.name" class="card-bg-image" />
          <h3 class="room-name">{{ room.name }}</h3>
          <span class="new-arrivals-tag">New arrivals</span>
        </div>
      </div>
    </div>
    <div class="pagination-controls">
      <span class="page-info">01 / 05</span>
      <a href="#" class="next-link">Next <span class="arrow">›</span></a>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface Room {
  name: string;
  image: string;
}

const rooms = ref<Room[]>([
  { name: "Bedroom", image: "/images/bed-room-card.png" },
  { name: "Living room", image: "/images/living-room-card.jpg" },
]);

// Placeholder for pagination logic if needed later
const currentPage = ref(1);
const totalPages = ref(5);
</script>

<style scoped>
.find-room-section {
  background-color: var(--bg-main);
  padding: 80px 0 100px 0; /* Added more bottom padding */
  font-family: var(--font-sans);
}

.container {
  max-width: 1280px; /* ou ce que tu préfères */
  margin: 0 auto;
  position: relative;
}

.section-title {
  font-family: var(--font-serif);
  font-size: 55px; /* Slightly adjusted size */
  color: var(--text-secondary);
  text-align: left;
  margin-bottom: 55px; /* Adjusted space */
  font-weight: 400; /* Design looks like a regular, not heavy bold */
  line-height: 60px;
}

.room-showcase {
  display: flex;
  gap: 12px; /* Gap between info column and cards column */
}

.showcase-info {
  flex-basis: 22%; /* Adjusted basis for the left info column */
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Pushes info-text up, pagination-controls down */
  color: var(--text-secondary);
  padding-top: 5px; /* Slight adjustment to visually align top of text with top of cards */
}

.info-text {
  font-size: 14px;
  line-height: 1.75;
  margin-bottom: 25px; /* Space before pagination might be needed if content is short */
  color: var(--text-secondary);
}

.pagination-controls {
  display: flex;
  justify-content: flex-start; /* This is CRUCIAL for separating page-info and next-link */
  gap: 8px;
  align-items: center;
  font-size: 18px;
}

.page-info {
  color: var(--text-secondary);
  font-size: 18px;
  font-weight: 400;
  line-height: 25px;
  letter-spacing: 0;
  opacity: 50%;
}

.next-link {
  text-decoration: none;
  color: var(--text-primary);
  font-weight: 700; /* Slightly bolder */
  display: flex;
  align-items: center;
  font-size: 20px;
  line-height: 25px;
}

.next-link .arrow {
  margin-left: 10px;
  font-size: 22px;
  line-height: 1; /* Helps with vertical alignment */
}

.room-cards-container {
  flex-basis: 78%; /* Adjusted basis for the cards area */
  display: flex;
  gap: 35px; /* Space between the two room cards */
}

.room-card {
  flex: 1; /* Each card takes equal space */
  display: flex;
  position: relative; /* Crucial for absolute positioning of overlay children */
  aspect-ratio: 3 / 4.2; /* Making cards slightly taller (width / height) */
  overflow: hidden;
  justify-content: space-between;
}

.card-bg-image {
  width: 70%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.new-arrivals-tag {
  font-size: 18px; /* Smaller as in design */
  color: var(--text-secondary);
  font-weight: 400;
  line-height: 25px; /* Adjusted line height for multi-line room names */
  white-space: nowrap; /* Prevent wrapping if container is too narrow */
}

.room-name {
  font-family: var(--font-serif);
  font-size: 55px; /* Adjusted size to match design */
  color: var(--text-primary);
  text-align: center;
  font-weight: 400; /* Bolder for emphasis */
  line-height: 60px; /* Adjusted line height for multi-line room names */
  letter-spacing: -0.6px;
  width: 70%;
  text-wrap: wrap;
  max-width: 40%;
  position: absolute;
  top: 50%;
  left: 65%;
  transform: translate(-50%, -50%);
}

/* Responsive Adjustments */
@media (max-width: 1024px) {
  /* Added a breakpoint for tablets */
  .container {
    padding: 0 3%;
  }
  .section-title {
    font-size: 50px;
  }
  .showcase-info {
    flex-basis: 25%;
  }
  .room-cards-container {
    flex-basis: 75%;
    gap: 30px;
  }
  .room-name {
    font-size: 40px;
  }
  .new-arrivals-tag {
    font-size: 10px;
  }
}

@media (max-width: 768px) {
  /* Mobile devices */
  .find-room-section {
    padding: 60px 0 80px 0;
  }
  .container {
    padding: 0 5%;
  }
  .section-title {
    font-size: 40px; /* Smaller for mobile */
    text-align: center;
    margin-bottom: 40px;
  }
  .room-showcase {
    flex-direction: column; /* Stack elements */
    gap: 30px;
  }
  .showcase-info,
  .room-cards-container {
    flex-basis: auto; /* Full width when stacked */
    width: 100%;
  }
  .showcase-info {
    align-items: center; /* Center info text on mobile */
    text-align: center;
    padding-bottom: 20px; /* Space before cards */
  }
  .pagination-controls {
    /* width: 100%; */ /* Already set */
    padding: 0 10px; /* Add some internal padding if text is too close to edges */
  }
  .info-text {
    font-size: 18px;
    font-weight: 400;
    line-height: 25px;
  }
  .room-cards-container {
    flex-direction: column;
    gap: 25px;
  }
  .room-card {
    aspect-ratio: 1.1 / 1; /* Slightly wider than tall, or square (1/1) */
  }
  .room-name {
    font-size: 34px;
  }
  .card-overlay {
    padding: 18px;
  }
  .new-arrivals-tag {
    top: 18px; /* Match new padding */
  }
}
</style>
