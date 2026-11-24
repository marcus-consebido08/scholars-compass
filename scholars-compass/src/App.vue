<script setup>
import { ref } from 'vue'
import LandingPage from './components/LandingPage.vue'

const surveySection = ref(null)

function scrollToSurvey() {
  surveySection.value?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <main>
    <LandingPage @start-survey="scrollToSurvey" />

    <section ref="surveySection" class="survey-placeholder">
      <h2>Preference Survey (Next Milestone)</h2>
      <p>
        This section will hold the college preference questions that filter matching schools
        and open the map + college list view.
      </p>
    </section>
  </main>
</template>

<style scoped>
.survey-placeholder {
  max-width: 1040px;
  margin: 24px auto 0;
  padding: 36px 24px;
  border-top: 2px dashed #cbd5e1;
  color: #475569;
  font-family: system-ui, -apple-system, sans-serif;
}

.survey-placeholder h2 {
  margin: 0 0 8px;
  color: #1e293b;
  font-size: 1.3rem;
}

.survey-placeholder p {
  margin: 0;
}
</style>