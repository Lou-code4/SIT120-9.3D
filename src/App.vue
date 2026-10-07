<script setup>
import { ref } from 'vue'
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import ContactForm from './components/ContactForm.vue'
import HomeView from './views/HomeView.vue'
import CafesView from './views/CafesView.vue'
import CafeDetailsView from './views/CafeDetailsView.vue'

const activePage = ref('home')
const submittedData = ref(null)
const selectedCafe = ref('moss')

const drinkLabels = {
  classic: 'Classic matcha',
  iced: 'Iced matcha latte',
  strawberry: 'Strawberry matcha',
  fruit: 'Fruit matcha'
}

function navigate(page) {
  activePage.value = page
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function handleCafeSelection(cafeId) {
  selectedCafe.value = cafeId
  navigate('details')
}

function handleFormSubmission(payload) {
  submittedData.value = payload
}
</script>

<template>
  <AppHeader :active-page="activePage" @navigate="navigate" />

  <HomeView v-if="activePage === 'home'" @navigate="navigate" />
  <CafesView v-else-if="activePage === 'cafes'" @navigate="navigate" @select-cafe="handleCafeSelection" />
  <CafeDetailsView v-else-if="activePage === 'details'" :cafe-id="selectedCafe" @navigate="navigate" />

  <template v-else>
    <ContactForm
      form-title="Tell us what you need from your next matcha cafe."
      initial-name=""
      @submit-form="handleFormSubmission"
    />

    <section v-if="submittedData" class="acknowledgement-card" aria-live="polite">
      <p class="eyebrow">Submission received</p>
      <h3>Your matcha preferences</h3>
      <p><strong>Thanks, {{ submittedData.name }}.</strong> Your preferences have been saved on this page.</p>
      <ul>
        <li><strong>Email:</strong> {{ submittedData.email }}</li>
        <li><strong>Preferred suburb:</strong> {{ submittedData.suburb }}</li>
        <li><strong>Drink type:</strong> {{ drinkLabels[submittedData.drinkType] }}</li>
        <li><strong>Sweetness:</strong> {{ submittedData.sweetness }} / 100</li>
        <li><strong>Visit purpose:</strong> {{ submittedData.purpose }}</li>
        <li><strong>Helpful features:</strong> {{ submittedData.features.length ? submittedData.features.join(', ') : 'None selected' }}</li>
      </ul>
    </section>
  </template>

  <AppFooter :active-page="activePage" @navigate="navigate" />
</template>
