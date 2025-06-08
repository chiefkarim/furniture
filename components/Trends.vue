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
          <div class="slider-track">
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
          <div class="trends-carousel">
            <UCarousel
              ref="carouselRef"
              v-slot="{ item: image }"
              :align="'start'"
              :items="inspirationImages"
              :slidesToScroll="2"
              :ui="{
                item: 'basis-[37%]',
                container: 'gap-[30px]',
              }"
              class="inspiration-image-wrapper"
            >
              <div class="inspiration-image-card">
                <img :src="image.src" :alt="image.alt" />
              </div>
              <p class="inspiration-name">{{ image.name }}</p>
            </UCarousel>
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
            <div>
              <div class="inspiration-pagination">
                <button
                  class="nav-arrow prev-arrow"
                  @click="goPrev"
                  aria-label="Previous inspiration"
                >
                  <img src="/images/left-arrow.svg" />
                </button>
                <button
                  class="nav-arrow next-arrow"
                  @click="goNext"
                  aria-label="Next inspiration"
                >
                  <img src="/images/right-arrow.svg" />
                </button>
              </div>
              <span class="page-info">
                {{ formattedCurrentSlide }} / {{ formattedTotalSlides }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from "vue";

const email = ref("");
const carouselRef = ref();
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

// 3. Calcul du nombre total de slides possibles
const totalSlides = ref(0);
function formatSlideNumber(n: number): string {
  return n < 10 ? "0" + n : String(n);
}

const formattedCurrentSlide = computed(() =>
  formatSlideNumber(currentIndex.value + 1),
);
const formattedTotalSlides = computed(() =>
  formatSlideNumber(totalSlides.value),
);

onMounted(() => {
  if (carouselRef.value) {
    totalSlides.value = carouselRef.value.emblaApi.scrollSnapList().length;

    carouselRef.value.emblaApi.on("select", () => {
      currentIndex.value = carouselRef.value.emblaApi.selectedScrollSnap();
    });
  }
});

onUnmounted(() => {
  if (carouselRef.value) {
    carouselRef.value.emblaApi.off("select");
  }
});

// 7. Navigation “Prev” / “Next”
function goNext() {
  if (carouselRef.value) {
    carouselRef.value.emblaApi.scrollNext();
  }
}

function goPrev() {
  if (carouselRef.value) {
    carouselRef.value.emblaApi.scrollPrev();
  }
}

// 9. Formulaire d’abonnement (inchangé)
function handleSubscription() {
  if (email.value) {
    alert(`Subscribed with: ${email.value}`);
    email.value = "";
  }
}
</script>

<style scoped>
.latest-trends-section {
  background-color: white;
  font-family: var(--font-sans);
  padding: 48px 0;
}
.container {
  max-width: 1444px;
  margin: 0 auto;
  position: relative;
}
.slider-track {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.trends-subscription {
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.trends-info {
  flex-basis: auto;
}
.trends-info h2 {
  font-family: var(--font-serif);
  font-size: 35px;
  color: var(--on-background-primary);
  line-height: 40px;
  font-weight: 400;
  margin-bottom: 16px;
  text-align: left;
  letter-spacing: -0.3px;
}
.trends-info p {
  font-size: 18px;
  color: var(--brown-light);
  font-weight: 400;
  line-height: 25px;
  margin-bottom: 16px;
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
  padding: 15px 15px;
  border: 1px solid var(--light-border-color, #ddd);
  font-family: var(--font-sans);
  font-size: 18px;
  background-color: #f3eee84d;
  color: #00000073;
  outline: none;
  border-radius: 0;
  height: 50px;
  line-height: 25px;
  font-weight: 400;
}
.subscription-form input[type="email"]::placeholder {
  color: var(--brown-light);
}
.subscription-form button[type="submit"] {
  padding: 12px 29px;
  background-color: var(--brown-dark);
  color: var(--white);
  border: 1px solid var(--text-secondary);
  cursor: pointer;
  font-family: "Karla";
  font-size: 17px;
  height: 50px;
  font-weight: 700;
  line-height: 25px;
  letter-spacing: 0.3px;
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
  margin-bottom: 0;
  font-size: 15px;
  font-family: "Lato";
  text-transform: capitalize;
  color: var(--on-background-primary);
  font-weight: 400;
  text-align: left;
  line-height: 20px;
  margin-top: 15px;
}

.inspiration-text-content {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-top: 64px;
  margin-bottom: 40px;
  text-align: left;
}

.inspirations-title {
  font-family: var(--font-serif);
  font-size: 35px;
  color: var(--brown-dark);
  line-height: 40px;
  letter-spacing: -0.3px;
  font-weight: 400;
  text-align: left;
}
.inspirations-description {
  font-size: 18px;
  line-height: 25px;
  color: var(--brown-light);
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
  gap: 11px;
  margin-bottom: 20px;
}

.page-info {
  font-size: 18px;
  color: var(--brown-light);
  line-height: 25px;
  letter-spacing: 0;
  font-weight: 400;
}
.inspiration-image-wrapper {
  flex: 0 0 calc(100% / 2.5);
  box-sizing: border-box;
  text-align: left;
}
.trends-carousel {
  display: none;
}
/* ----------------------------------------------------------- */
/*                Styles “Desktop & Large Tablet”              */
/*      (≥ 992px : on bascule sur le slider horizontal)        */
/* ----------------------------------------------------------- */
@media (min-width: 992px) {
  /* On masque la grille mobile/tablet */
  .latest-trends-section {
    padding: 70px clamp(1rem, 5vw, 6.5rem);
  }
  .trends-carousel {
    display: block;
  }
  .inspiration-images {
    display: none;
  }
  .inspirations-showcase {
    flex-flow: column;
  }

  /* 1. Viewport du slider */
  .slider-viewport {
    display: block;
    width: 100%;
    overflow: hidden;
    position: relative;
  }

  /* 2. Track contenant toutes les cartes en flex-row */
  .slider-track {
    display: none;
    transition: transform 0.5s ease;
    gap: 40px;
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
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    width: 40px;
    height: 40px;
    background-color: transparent;
  }

  /* 5. Texte & disposition texte à droite */
  .inspiration-text-content {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 40px;
    align-items: flex-start;
    margin-top: 40px;
    margin-bottom: 0;
  }
  .inspirations-title {
    font-family: var(--font-serif);
    font-size: 45px;
    color: var(--brown-dark);
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
    align-items: center;
    gap: 20px;
  }

  .inspiration-name {
    display: none;
  }
  .trends-subscription {
    margin-bottom: 64px;
    flex-direction: row;
    justify-content: space-between;
  }

  .subscription-form {
    flex-direction: row;
    align-items: center;
    max-width: none;
    width: auto;
  }
  .subscription-form input[type="email"] {
    min-width: 266px;
  }
}
</style>
