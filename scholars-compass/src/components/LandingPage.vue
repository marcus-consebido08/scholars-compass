<script setup>
// Emits an event to App.vue when "Get Started" is clicked
const emit = defineEmits(['start-survey'])
</script>

<template>
  <div class="page-wrapper">
    <!-- ==================== HERO SECTION (SINGLE COLUMN) ==================== -->
    <section id="home" class="hero">
      <h1 class="title">Scholar’s Compass</h1>

      <p class="tagline">“Dream it. Explore it. Find your future.”</p>

      <p class="description">
        Every great future starts with an important step. Scholar’s Compass is a student-centered
        platform that aims to guide aspiring college students in exploring different college courses
        and campuses that aligns with their interest, abilities, and aspirations. Discover your
        options, find the path that suits your goals and select your better future. Start creating
        your college journey with what your heart truly desires.
      </p>

      <button class="cta-button" @click="emit('start-survey')">Get Started</button>
    </section>
  </div>
</template>

<style scoped>
/* Base Page Container */
.page-wrapper {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #8fa1b5;
  color: #ffffff;
  font-family: Georgia, 'Times New Roman', serif;
}

/* ==================== HERO STYLES ==================== */
.hero {
  flex: 1;
  max-width: 820px;
  margin: 0 auto;
  padding: 72px 24px 80px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.title {
  font-size: clamp(2.5rem, 6vw, 4.25rem);
  font-weight: 700;
  margin: 0 0 12px;
  line-height: 1.1;
}

.tagline {
  font-size: clamp(1.1rem, 2.2vw, 1.45rem);
  font-style: italic;
  font-weight: 700;
  margin: 0 0 28px;
}

.description {
  max-width: 650px;
  font-size: 1.05rem;
  line-height: 1.65;
  margin: 0 0 36px;
}

.cta-button {
  background-color: #ffb300;
  color: #ffffff;
  border: none;
  border-radius: 999px;
  padding: 14px 48px;
  font-size: 1.15rem;
  font-family: Georgia, 'Times New Roman', serif;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;
}

.cta-button:hover {
  background-color: #db930d;
}

.cta-button:active {
  transform: scale(0.98);
}

</style>