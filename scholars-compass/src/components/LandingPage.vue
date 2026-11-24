<script setup>
import { ref } from 'vue'
import logoUrl from '../assets/LOGO.jpg'

// Emits an event to App.vue when "Get Started" is clicked
const emit = defineEmits(['start-survey'])

// Holds whatever the user types in the top search bar
const searchQuery = ref('')

function handleSearch() {
  if (!searchQuery.value.trim()) return
  alert(`Search preview: "${searchQuery.value}" (We will connect this to college data later!)`)
}
</script>

<template>
  <div class="page-wrapper">
    <!-- ==================== TOP NAVBAR ==================== -->
    <header class="navbar">
      <div class="nav-left">
        <div class="logo-circle">
          <img class="logo-image" :src="logoUrl" alt="Scholar Compass logo" />
        </div>
        <a href="#login" class="login-link">Log in</a>
      </div>

      <!-- Center Search Bar -->
      <form class="search-form" @submit.prevent="handleSearch">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search"
          aria-label="Search colleges"
        />
      </form>

      <!-- Right Navigation Links -->
      <nav class="nav-right">
        <a href="#home">Home</a>
        <a href="#features">Features</a>
        <a href="#about">About</a>
      </nav>
    </header>

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

/* ==================== NAVBAR STYLES ==================== */
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 14px 28px;
  background-color: #464d6b;
}

.nav-left {
  display: flex;
  align-items: center;
  gap: 18px;
}

.logo-circle {
  width: 52px;
  height: 52px;
  border-radius: 50%;
  background-color: #163366;
  color: #ffffff;
  font-size: 0.75rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  letter-spacing: 0.05em;
  flex-shrink: 0;
  overflow: hidden;
}

.logo-image {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.login-link,
.nav-right a {
  color: #ffffff;
  text-decoration: none;
  font-weight: 700;
  font-size: 1.05rem;
}

.login-link:hover,
.nav-right a:hover {
  text-decoration: underline;
}

.search-form {
  flex: 1;
  max-width: 460px;
}

.search-form input {
  width: 100%;
  padding: 10px 18px;
  border: none;
  border-radius: 999px;
  background-color: #d6d9de;
  color: #1e293b;
  font-size: 0.95rem;
  font-family: system-ui, -apple-system, sans-serif;
  outline: none;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 24px;
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

/* Mobile responsiveness so nothing breaks on smaller screens */
@media (max-width: 768px) {
  .navbar {
    flex-wrap: wrap;
    padding: 14px 16px;
  }

  .search-form {
    order: 3;
    max-width: 100%;
    flex-basis: 100%;
  }
}
</style>