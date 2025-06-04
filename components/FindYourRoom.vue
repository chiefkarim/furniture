<template>
  <section class="find-room-section container">
    <!-- Titre principal -->
    <h2 class="section-title">Find your room</h2>
    <!-- Sous-texte sous le titre -->
    <p class="info-text">
      Dining room, bedroom, bathroom or office. Find what you need
    </p>

    <!-- Conteneur des cartes -->
    <div class="room-cards-container">
      <div v-for="room in visibleRooms" :key="room.name" class="room-card">
        <!-- Partie “Image + nom de la pièce” -->
        <div class="image-wrapper">
          <img :src="room.image" :alt="room.name" class="card-bg-image" />
          <!-- Nom de la pièce, centré sur l’image -->
          <h3 class="room-name">{{ room.name }}</h3>
        </div>

        <!-- Partie “News arrivals” à droite de l’image -->
        <div class="news-wrapper">
          <span class="news-arrivals-tag">News arrivals</span>
        </div>
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

// 1. Données statiques (exemple)
const rooms = ref<Room[]>([
  { name: "Bedroom", image: "/images/bed-room-card.png" },
  { name: "Living room", image: "/images/living-room-card.jpg" },
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
  const newCount = window.innerWidth < 768 ? 1 : 2;
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
});

onUnmounted(() => {
  window.removeEventListener("resize", updateItemsPerPage);
});

// 6. Fonction "Next" pour la pagination
function goNext() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  } else {
    currentPage.value = 1;
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
  padding: 60px 7%;
  font-family: "Helvetica Neue", Arial, sans-serif;
}

/* Centrage et largeur max (identique à la capture) */
.container {
  max-width: 500px; /* Pour correspondre exactement à la largeur mobile de la photo */
  margin: 0 auto;
}

/* Titre principal */
.section-title {
  font-family: "Georgia", serif;
  font-size: 32px;
  font-weight: 400;
  line-height: 1.2;
  color: #4a4131;
  margin-bottom: 12px;
}

/* Sous-texte sous le titre */
.info-text {
  font-size: 14px;
  font-weight: 400;
  line-height: 1.75;
  color: #8a8175;
  margin-bottom: 24px;
}

/* Conteneur des cartes, en colonne par défaut (mobile) */
.room-cards-container {
  display: flex;
  flex-direction: column;
  gap: 24px;
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
  overflow: hidden;
  background-color: #ffffff; /* On peut garder un fond blanc derrière l’image */
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
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: "Georgia", serif;
  font-size: 28px;
  color: #a15c4a;
  font-weight: 400;
  line-height: 1.1;
  text-align: center;
  text-shadow: 0px 1px 2px rgba(0, 0, 0, 0.2);
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
  font-size: 12px;
  font-weight: 400;
  color: #8a8175;
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
  color: #a15c4a;
  display: flex;
  align-items: center;
}

.next-link .arrow {
  margin-left: 6px;
  font-size: 18px;
}

/* Texte “01 / 05” */
.page-info {
  font-size: 14px;
  font-weight: 400;
  color: #8a8175;
  opacity: 0.6;
}

/* ---- Responsive Desktop (≥ 768px) pour 2 cartes côte à côte ---- */
@media (min-width: 768px) {
  .container {
    max-width: 1280px; /* On agrandit pour afficher deux cartes */
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }

  .room-cards-container {
    flex-direction: row;
    gap: 16px;
  }

  .room-card {
    flex: 1;
  }

  /* Ajuster taille du titre sur desktop */
  .section-title {
    font-size: 44px;
  }
  .info-text {
    font-size: 16px;
    margin-bottom: 32px;
  }
}
</style>
