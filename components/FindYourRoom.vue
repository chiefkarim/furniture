<template>
  <section id="rooms" class="find-room-section container">
    <!-- Titre principal -->
    <h2 class="section-title">Find your room</h2>

    <!-- Conteneur des cartes -->
    <div class="room-cards-container">
      <p class="info-text">
        Dining room,<br />
        bedroom, bathroom <br />
        or office. Find what<br />
        you need
      </p>
      <!-- TODO: add loadeing indicators on the imags or have placeholders -->
      <div class="">
        <UCarousel
          ref="carouselRef"
          v-slot="{ item: room, index }"
          loop
          :align="'start'"
          :items="rooms"
          :ui="{
            item: 'basis-full  md:basis-1/2 shrink-0',
          }"
        >
          <div class="room-card">
            <div class="image-wrapper">
              <img :src="room.image" :alt="room.name" class="card-bg-image" />
              <h3 class="room-name" v-html="room.name"></h3>
            </div>
            <div class="news-wrapper">
              <span class="news-arrivals-tag">News arrivals</span>
            </div>
          </div>
        </UCarousel>
        <button class="next-link" @click.prevent="goNext">
          Next <span class="arrow">›</span>
        </button>
      </div>
    </div>

    <!-- Pagination / Contrôles en bas -->
    <div class="pagination-controls">
      <button class="next-link" @click.prevent="goNext">
        Next <span class="arrow">›</span>
      </button>
      <span class="page-info">
        {{ formattedCurrentPage }} / {{ formattedTotalPages }}
      </span>
    </div>
  </section>
</template>
<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from "vue";
// Définir le type Room
interface Room {
  name: string;
  image: string;
}

const carouselRef = ref();
// 1. Données statiques (exemple)
const rooms = ref<Room[]>([
  { name: "Bedroom", image: "/images/bed-room-card.png" },
  { name: "Living<br/>room", image: "/images/living-room-card.jpg" },
  { name: "Bedroom 2", image: "/images/bed-room-card.png" },
  { name: "Living<br/>room 2", image: "/images/living-room-card.jpg" },
]);

// 2. Pagination
const currentPage = ref(1);
// itemsPerPage ne repose plus sur window.innerWidth dès l'initialisation
const itemsPerPage = ref(2);

// 3. Calcul du nombre total de pages
const totalPages = computed(() => {
  return Math.ceil(rooms.value.length / itemsPerPage.value);
});

// 4. Sélection des salles à afficher selon la page
const visibleRooms = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage.value;
  return rooms.value.slice(start, start + itemsPerPage.value);
});

// 5. Mettre à jour itemsPerPage au redimensionnement, uniquement côté client
function updateItemsPerPage() {
  const newCount = window.innerWidth < 992 ? 1 : 2;
  if (newCount !== itemsPerPage.value) {
    itemsPerPage.value = newCount;
    if (currentPage.value > totalPages.value) {
      currentPage.value = totalPages.value;
    }
  }
}

onMounted(() => {
  // On attend que le composant soit monté pour accéder à window
  updateItemsPerPage();
  window.addEventListener("resize", updateItemsPerPage);

  if (carouselRef.value)
    carouselRef.value.emblaApi.on("select", () => {
      if (currentPage.value < totalPages.value) {
        currentPage.value++;
      } else {
        currentPage.value = 1;
      }
    });
});

onUnmounted(() => {
  window.removeEventListener("resize", updateItemsPerPage);
});

// 6. Fonction "Next" pour la pagination
function goNext() {
  if (carouselRef.value) {
    carouselRef.value.emblaApi.scrollNext();
  }
}

// 7. Formatage pour afficher deux chiffres si < 10
const formattedCurrentPage = computed(() => {
  return currentPage.value < 10
    ? "0" + currentPage.value
    : String(currentPage.value);
});
const formattedTotalPages = computed(() => {
  return totalPages.value < 10
    ? "0" + totalPages.value
    : String(totalPages.value);
});
</script>

<style scoped>
/* Fond principal (beige clair) */
.find-room-section {
  background-color: #f3efe8;
  padding: 48px clamp(1rem, 5vw, 6.5rem);
  font-family: var(--font-sans);
}

/* Centrage et largeur max (identique à la capture) */
.container {
  margin: 0 auto;
}

/* Titre principal */
.section-title {
  font-family: var(--font-serif);
  font-size: 32px;
  font-weight: 400;
  line-height: 1.2;
  color: var(--brown-dark);
  margin-bottom: 0;
}

/* Sous-texte sous le titre */
.info-text {
  width: 100%;
  font-size: 18px;
  font-weight: 400;
  line-height: 25px;
  color: var(--light-brown);
  letter-spacing: 0px;
  margin-top: 0;
}

/* Conteneur des cartes, en colonne par défaut (mobile) */
.room-cards-container {
  display: flex;
  flex-direction: column;
  gap: 24px;
  margin-top: 20px;
}

/* Chaque carte devient un flex-row (image à gauche, texte à droite) */
.room-card {
  display: flex;
  flex-direction: row;
  background-color: transparent; /* Le fond beige est celui de .find-room-section */
  align-items: flex-start;
}

/* Partie gauche : l’image et le titre de la pièce */
.image-wrapper {
  position: relative;
  flex-shrink: 0;
  width: 60%; /* 60% de la largeur de la carte */
  aspect-ratio: 3 / 4.2; /* Même ratio que sur la photo */
  border-radius: 1px;
}

/* L’image elle-même */
.card-bg-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

/* Nom de la pièce, centré sur l’image */
.room-name {
  position: absolute;
  top: 50%;
  right: 1%;
  transform: translate(35%, -50%);
  font-family: var(--font-serif);
  font-weight: 400;
  font-size: 35px;
  color: var(--text-primary);
  font-weight: 400;
  line-height: 40px;
  letter-spacing: -0.3px;
  text-align: center;
  pointer-events: none; /* Pour s’assurer qu’on ne clique pas sur le texte */
}

/* Partie droite : “News arrivals” */
.news-wrapper {
  flex: 1;
  display: flex;
  align-items: flex-start; /* En haut */
  justify-content: flex-start;
  padding-left: 16px; /* Un petit espace entre l’image et le texte */
}

/* Style du label “News arrivals” */
.news-arrivals-tag {
  font-size: 18px;
  font-weight: 400;
  line-height: 25px;
  letter-spacing: 0px;
  color: #00000073;
  background-color: transparent; /* Sur fond beige clair du conteneur parent */
}

/* Pagination / contrôles en bas */
.pagination-controls {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 24px;
}

/* Bouton “Next ›” */
.next-link {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
  font-size: 16px;
  font-weight: 700;
  color: var(--text-primary);
  display: flex;
  align-items: center;
}

.next-link .arrow {
  margin-left: 6px;
  font-size: 18px;
}

/* Texte “01 / 05” */
.page-info {
  font-size: 18px;
  font-weight: 400;
  color: var(--brown-light);
  line-height: 25px;
  letter-spacing: 0;
}
.room-cards-container .next-link {
  display: none;
}
/* ---- Responsive Desktop (≥ 768px) pour 2 cartes côte à côte ---- */
@media (min-width: 992px) {
  .container {
    max-width: 1444px;
    margin: 0 auto;
    position: relative;
    padding: 70px clamp(1rem, 5vw, 6.5rem);
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  .room-cards-container {
    flex-direction: row;
    gap: 16px;

    margin-top: 48px;
  }

  .room-card {
    flex: 1;
  }
  .room-name {
    font-size: 55px;
    letter-spacing: -0.6px;
    line-height: 60px;
  }
  /* Ajuster taille du titre sur desktop */
  .section-title {
    font-size: 55px;
    line-height: 60px;
    letter-spacing: -0.6px;
    color: var(--text-secondary);
  }
  .pagination-controls {
    margin-top: 48px;
    width: 20%;
  }
  .room-cards-container .next-link {
    display: block;
    position: absolute;
    bottom: 70px;
  }
  .pagination-controls .next-link {
    display: none;
  }
  .news-arrivals-tag {
    color: var(--brown-light);
  }
  .info-text {
    width: auto;
    flex-shrink: 0;
  }
}
</style>
