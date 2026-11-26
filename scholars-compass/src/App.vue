<script setup>
import { ref } from 'vue'
import collegesData from './data/Colleges.json'
import logoUrl from './assets/LogoTr.png'
import LandingPage from './components/LandingPage.vue'
import MapSect from './components/MapSect.vue'
import SurveySect from './components/SurveySect.vue'
import AboutSect from './components/AboutSect.vue'

const colleges = collegesData
const selectedCollege = ref(null)
const searchQuery = ref('')

function scrollToSurvey() {
  document.getElementById('survey')?.scrollIntoView({ behavior: 'smooth' })
}

function handleSelectCollege(college) {
  selectedCollege.value = college
}

function handleSearch() {
  const query = searchQuery.value.trim().toLowerCase()
  if (!query) return

  const match = colleges.find((college) => college.name.toLowerCase().includes(query))
  if (!match) {
    alert(`No matching pin yet for "${searchQuery.value}".`)
    return
  }

  handleSelectCollege(match)
  document.getElementById('map-section')?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <header class="navbar">
    <div class="nav-left">
      <div class="logo-circle">
        <img class="logo-image" :src="logoUrl" alt="Scholar Compass logo" />
      </div>
      <a href="#login" class="login-link">Log in</a>
    </div>

    <form class="search-form" @submit.prevent="handleSearch">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search"
        aria-label="Search colleges"
      />
    </form>

    <nav class="nav-right">
      <a href="#home">Home</a>
      <a href="#survey" @click.prevent="scrollToSurvey">Survey</a>
      <a href="#about">About</a>
    </nav>
  </header>

  <main>
    <div class="hero-map-layout">
      <LandingPage @start-survey="scrollToSurvey" />
      <MapSect
        :colleges="colleges"
        :selected-college="selectedCollege"
        @select-college="handleSelectCollege"
      />
    </div>
    <SurveySect />
    <AboutSect />
  </main>
</template>

<style scoped>
.hero-map-layout {
  min-height: calc(100vh - 80px);
  display: grid;
  grid-template-columns: minmax(0, 1.1fr) minmax(300px, 0.9fr);
  align-items: center;
  gap: clamp(24px, 4vw, 56px);
  padding: 40px clamp(24px, 5vw, 72px);
  background-color: #8b9ab1;
}

.hero-map-layout > * {
  min-width: 0;
}

.navbar {
  position: sticky;
  top: 0;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 14px 28px;
  background-color: #464d6b;
  font-family: Georgia, 'Times New Roman', serif;
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
  background-color: #464d6b;
  display: flex;
  align-items: center;
  justify-content: center;
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

  .hero-map-layout {
    min-height: 0;
    grid-template-columns: 1fr;
    gap: 16px;
    padding: 32px 20px 48px;
  }
}
</style>
