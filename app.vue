<template>
  <AppHeader />

  <FindYourRoom />
  <About />
  <Trends />
  <!-- You can add other page content below the header -->
  <!--
    <main>
      <p>Page content goes here...</p>
    </main>
    -->
</template>

<script setup lang="ts">
// Components are auto-imported in Nuxt 3 if placed in the `components/` directory
// So no explicit import for AppHeader is needed here.
</script>

<style>
/* Global styles if any - e.g., body reset */
/*
 .container {
  max-width: 1280px; 
  margin: 0 auto;
  position: relative;
}
*/
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Lato", sans-serif; /* Default body font */
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
</style>
