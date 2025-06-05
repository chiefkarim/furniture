<template>
  <div class="latest-trends-section">
    <section class="container">
      <div class="trends-subscription">
        <div class="trends-info">
          <h2>Be aware of the latest trends</h2>
          <p>Stay informed of new trends, but also of our various offers.</p>
          <a href="#" class="learn-more-link">
            Learn more <span class="arrow">›</span>
          </a>
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
        <div class="slider-viewport">
          <div
            class="slider-track"
            :style="{ transform: `translateX(-${computedShift}%)` }"
          >
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
                @click="goPrev"
                aria-label="Previous inspiration"
              >
                ‹
              </button>
              <button
                class="nav-arrow next-arrow"
                @click="goNext"
                aria-label="Next inspiration"
              >
                ›
              </button>
            </div>
            <span class="page-info">
              {{ formattedCurrentSlide }} / {{ formattedTotalSlides }}
            </span>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from "vue";

const email = ref("");

// Données des images
interface Inspiration {
  name: string;
  src: string;
  alt: string;
}
const inspirationImages = ref<Inspiration[]>([
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

// 1. Index du slide actuel (0-based)
const currentIndex = ref(0);

// 2. Nombre d’items visibles : 2.5 en desktop, 1.5 en tablet/mobile large
const countVisible = ref(2.5);

// 3. Calcul du nombre total de slides possibles
const totalSlides = computed(() => {
  const n = inspirationImages.value.length;
  const maxIndex = Math.floor(n - countVisible.value);
  return maxIndex >= 0 ? maxIndex + 1 : 1;
});

// 4. Chaque carte occupe (100% / countVisible) → décalage en pourcentage
const slideShiftPercent = computed(() => {
  return 100 / countVisible.value;
});

// 5. Calcul du “shift” effectif selon l’index :
//    - Si ce n’est pas le dernier slide, shift = index * slideShiftPercent
//    - Si c’est le dernier slide, on veut que la dernière image soit entièrement visible → shift spécial
const computedShift = computed(() => {
  const n = inspirationImages.value.length;
  if (currentIndex.value < totalSlides.value - 1) {
    return currentIndex.value * slideShiftPercent.value;
  } else {
    // Décalage pour aligner la dernière image en bord droit
    // (n - countVisible) * (100 / countVisible)
    return (n - countVisible.value) * slideShiftPercent.value;
  }
});

// 6. Au redimensionnement, on ajuste countVisible
function updateCountVisible() {
  // < 768px → 1.5 cartes visibles, ≥ 768px → 2.5 cartes visibles
  const newCount = window.innerWidth < 768 ? 1.5 : 2.5;
  if (newCount !== countVisible.value) {
    countVisible.value = newCount;
    // Si l’index courant dépasse, on le recale
    if (currentIndex.value > totalSlides.value - 1) {
      currentIndex.value = totalSlides.value - 1;
    }
  }
}

onMounted(() => {
  updateCountVisible();
  window.addEventListener("resize", updateCountVisible);
});
onUnmounted(() => {
  window.removeEventListener("resize", updateCountVisible);
});

// 7. Navigation “Prev” / “Next”
function goNext() {
  if (currentIndex.value < totalSlides.value - 1) {
    currentIndex.value++;
  } else {
    currentIndex.value = 0;
  }
}
function goPrev() {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  } else {
    currentIndex.value = totalSlides.value - 1;
  }
}

// 8. Pagination formatée (“01” / “05”)
const formattedCurrentSlide = computed(() => {
  const display = currentIndex.value + 1;
  return display < 10 ? "0" + display : String(display);
});
const formattedTotalSlides = computed(() => {
  const total = totalSlides.value;
  return total < 10 ? "0" + total : String(total);
});

// 9. Formulaire d’abonnement (inchangé)
function handleSubscription() {
  if (email.value) {
    alert(`Subscribed with: ${email.value}`);
    email.value = "";
  }
}
</script>

<style scoped>
/* ----------------------------------------------------------- */
/*     Partie “Trending Subscription” (styles mobile originaux) */
/* ----------------------------------------------------------- */
.latest-trends-section {
  background-color: white;
  font-family: var(--font-sans);
}
.container {
  max-width: 1444px;
  margin: 0 auto;
  padding: 48px clamp(1rem, 5vw, 6.5rem);
  position: relative;
}
.slider-track {
  display: grid;
  grid-template-columns: 1fr 1fr;
}

.trends-subscription {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.trends-info {
  flex-basis: auto;
}
.trends-info h2 {
  font-family: var(--font-serif);
  font-size: 35px;
  color: #121212;
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
  max-width: 450px;
}
.learn-more-link {
  font-family: "Karla";
  font-size: 17px;
  color: var(--text-primary);
  text-decoration: none;
  font-weight: 700;
  line-height: 25px;
  display: inline-flex;
  align-items: center;
}
.learn-more-link .arrow {
  margin-left: 8px;
  font-size: 18px;
}

.subscription-form {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 320px;
  gap: 16px;
}
.subscription-form input[type="email"] {
  padding: 12px 15px;
  border: 1px solid var(--light-border-color, #ddd);
  font-family: var(--font-sans);
  font-size: 14px;
  background-color: #f3eee84d;
  color: var(--text-secondary);
  outline: none;
  border-radius: 0;
  line-height: 25px;
}
.subscription-form input[type="email"]::placeholder {
  color: #aaa;
}
.subscription-form button[type="submit"] {
  padding: 12px 25px;
  background-color: #534b42;
  color: var(--white);
  border: 1px solid var(--text-secondary);
  cursor: pointer;
  font-family: "Karla";
  font-size: 14px;
  font-weight: 700;
  line-height: 25px;
  white-space: nowrap;
  transition: background-color 0.3s ease;
  border-radius: 0;
}
.subscription-form button[type="submit"]:hover {
  background-color: #50483e;
}

/* ----------------------------------------------------------- */
/*  Partie “Inspirations” : grille mobile/​tablet (inchangée)   */
/* ----------------------------------------------------------- */
.inspirations-showcase {
  /* Pas de flex ni grid supplémentaire */
  display: flex;
  flex-direction: column;
  flex-flow: column-reverse;
  text-align: left;
}

/* Grille de base pour mobile et tablet */
.inspiration-images {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 15px;
  margin-bottom: 30px;
}
.inspiration-image-card {
  aspect-ratio: 1;
  overflow: hidden;
  border-radius: 1px;
}
.inspiration-image-card img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.inspiration-name {
  margin-top: 15px;
  font-size: 15px;
  font-family: "Lato";
  text-transform: capitalize;
  color: #121212;
  font-weight: 400;
  text-align: left;
  line-height: 20px;
}

.inspiration-text-content {
  display: flex;
  flex-direction: column;
  gap: 25px;
  margin-top: 64px;
  margin-bottom: 40px;
  text-align: left;
}

.inspirations-title {
  font-family: var(--font-serif);
  font-size: 35px;
  color: var(--text-secondary);
  line-height: 40px;
  letter-spacing: -0.3px;
  font-weight: 400;
  text-align: left;
}
.inspirations-description {
  font-size: 18px;
  line-height: 25px;
  color: var(--text-secondary);
  font-family: var(--font-sans);
  font-weight: 400;
  margin: 0;
  text-align: left;
}
.pagination-wrapper {
  display: none;
}
.inspiration-pagination {
  display: flex;
  align-items: center;
  gap: 10px;
}
.inspiration-pagination .nav-arrow,
.inspiration-pagination .next-arrow {
  width: 32px;
  height: 32px;
  font-size: 18px;
}
.inspiration-pagination .page-info {
  font-size: 14px;
  color: var(--text-secondary);
  opacity: 0.7;
}
.inspiration-image-wrapper {
  flex: 0 0 calc(100% / 2.5);
  box-sizing: border-box;
  padding-right: 16px;
  text-align: left;
}

/* ----------------------------------------------------------- */
/*                Styles “Desktop & Large Tablet”              */
/*      (≥ 992px : on bascule sur le slider horizontal)        */
/* ----------------------------------------------------------- */
@media (min-width: 992px) {
  /* On masque la grille mobile/tablet */

  .inspiration-images {
    display: none;
  }
  .inspirations-showcase {
    flex-flow: column;
  }
  .container {
    padding: 70px clamp(1rem, 5vw, 6.5rem);
  }
  /* 1. Viewport du slider */
  .slider-viewport {
    display: block;
    width: 100%;
    overflow: hidden;
    position: relative;
    margin-bottom: 24px;
  }

  /* 2. Track contenant toutes les cartes en flex-row */
  .slider-track {
    display: flex;
    transition: transform 0.5s ease;
  }

  .inspiration-image-card {
    aspect-ratio: 3 / 4;
    overflow: hidden;
    border-radius: 1px;
  }
  .inspiration-image-card img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  /* 4. Pagination du slider */
  .pagination-controls {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 16px;
    margin-bottom: 40px;
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
    margin-right: 8px;
  }
  .nav-arrow.next-arrow {
    margin-left: 8px;
  }
  .page-info {
    font-size: 14px;
    color: var(--text-secondary);
    opacity: 0.7;
  }

  /* 5. Texte & disposition texte à droite */
  .inspiration-text-content {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 40px;
    align-items: flex-start;
  }
  .inspirations-title {
    font-family: var(--font-serif);
    font-size: 45px;
    color: var(--text-secondary);
    line-height: 40px;
    letter-spacing: -0.3px;
    font-weight: 300;
    text-align: left;
  }
  .inspirations-description {
    font-size: 18px;
    line-height: 25px;
    color: var(--text-secondary);
    font-family: var(--font-sans);
    font-weight: 400;
    margin: 0;
  }
  .pagination-wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 20px;
  }
  .inspiration-pagination {
    margin-bottom: 20px;
  }
  .inspiration-name {
    display: none;
  }
  .trends-subscription {
    margin-bottom: 64px;
    flex-direction: row;
    justify-content: space-between;
  }
  .slider-track {
    display: flex;
  }
}
</style>
