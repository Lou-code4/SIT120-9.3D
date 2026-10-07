<script setup>
import { ref } from 'vue'

const props = defineProps({
  formTitle: {
    type: String,
    default: 'Tell us what you need from your next matcha cafe.'
  },
  initialName: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['submit-form'])

const drinkOptions = [
  { value: 'classic', label: 'Classic matcha' },
  { value: 'iced', label: 'Iced matcha latte' },
  { value: 'strawberry', label: 'Strawberry matcha' },
  { value: 'fruit', label: 'Fruit matcha' }
]

const form = ref(createInitialForm())
const errors = ref({})
const successMessage = ref('')
const emailInput = ref(null)

function createInitialForm() {
  return {
    name: props.initialName,
    email: '',
    suburb: '',
    drinkType: '',
    sweetness: null,
    purpose: '',
    features: []
  }
}

function validateForm() {
  const nextErrors = {}

  if (!form.value.name.trim()) nextErrors.name = 'Please enter your name.'
  const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/
  if (!emailPattern.test(form.value.email.trim())) nextErrors.email = 'Please enter a valid email address.'
  if (!form.value.suburb.trim()) nextErrors.suburb = 'Please enter a preferred suburb.'
  if (!form.value.drinkType) nextErrors.drinkType = 'Please choose a drink type.'

  if (form.value.sweetness === null || form.value.sweetness === '' || form.value.sweetness < 0 || form.value.sweetness > 100) {
    nextErrors.sweetness = 'Enter a sweetness level from 0 to 100.'
  }

  if (!form.value.purpose) nextErrors.purpose = 'Please choose a main visit purpose.'

  errors.value = nextErrors
  return Object.keys(nextErrors).length === 0
}

function submitForm() {
  const isValid = validateForm()

  if (form.value.email.trim() && emailInput.value?.validity.typeMismatch) {
    emailInput.value.reportValidity()
    return
  }

  if (!isValid) return

  emit('submit-form', { ...form.value })
  successMessage.value = 'Preferences submitted successfully.'

  window.setTimeout(() => {
    form.value = createInitialForm()
    errors.value = {}
    successMessage.value = ''
  }, 2000)
}
</script>

<template>
  <main>
    <section class="page-intro form-intro">
      <p class="eyebrow">Matcha preference form</p>
      <h2>{{ formTitle }}</h2>
      <p>
        Tell us a little about what you are looking for. The form collects
        relevant preferences that could be used to suggest a suitable cafe.
      </p>
      <p class="form-note"><strong>All fields are required unless marked optional.</strong></p>
    </section>

    <section class="section-block">
      <form class="preference-form" @submit.prevent="submitForm" novalidate>
        <fieldset>
          <legend>Personal details</legend>

          <div class="form-grid">
            <div class="form-field">
              <label for="name">Name <span class="required-mark" aria-hidden="true">*</span></label>
              <input id="name" v-model="form.name" type="text" required aria-required="true">
              <p v-if="errors.name" class="form-error">{{ errors.name }}</p>
            </div>

            <div class="form-field">
              <label for="email">Email <span class="required-mark" aria-hidden="true">*</span></label>
              <input ref="emailInput" id="email" v-model="form.email" type="email" placeholder="name@example.com" required aria-required="true">
              <p v-if="errors.email" class="form-error">{{ errors.email }}</p>
            </div>

            <div class="form-field form-field-wide">
              <label for="suburb">Preferred suburb <span class="required-mark" aria-hidden="true">*</span></label>
              <input id="suburb" v-model="form.suburb" type="text" placeholder="e.g. Carlton" required aria-required="true">
              <p v-if="errors.suburb" class="form-error">{{ errors.suburb }}</p>
            </div>
          </div>
        </fieldset>

        <fieldset>
          <legend>Matcha preferences</legend>

          <div class="form-grid">
            <div class="form-field">
              <label for="drink-type">Drink type <span class="required-mark" aria-hidden="true">*</span></label>
              <select id="drink-type" v-model="form.drinkType" required aria-required="true">
                <option value="" disabled>Choose a drink</option>
                <option v-for="option in drinkOptions" :key="option.value" :value="option.value">
                  {{ option.label }}
                </option>
              </select>
              <p v-if="errors.drinkType" class="form-error">{{ errors.drinkType }}</p>
            </div>

            <div class="form-field">
              <label for="sweetness">Preferred sweetness (0–100) <span class="required-mark" aria-hidden="true">*</span></label>
              <input
                id="sweetness"
                v-model.number="form.sweetness"
                type="number"
                min="0"
                max="100"
                step="1"
                placeholder="0–100"
                required
                aria-required="true"
              >
              <p v-if="errors.sweetness" class="form-error">{{ errors.sweetness }}</p>
            </div>

            <div class="form-field form-field-wide">
              <span class="field-label">Main visit purpose <span class="required-mark" aria-hidden="true">*</span></span>
              <div class="choice-group">
                <label>
                  <input v-model="form.purpose" type="radio" name="purpose" value="Study">
                  Study
                </label>
                <label>
                  <input v-model="form.purpose" type="radio" name="purpose" value="Meet friends">
                  Meet friends
                </label>
                <label>
                  <input v-model="form.purpose" type="radio" name="purpose" value="Takeaway">
                  Takeaway
                </label>
              </div>
              <p v-if="errors.purpose" class="form-error">{{ errors.purpose }}</p>
            </div>

            <div class="form-field form-field-wide">
              <span class="field-label">Helpful cafe features (optional)</span>
              <div class="choice-group">
                <label>
                  <input v-model="form.features" type="checkbox" value="Wi-Fi">
                  Wi-Fi
                </label>
                <label>
                  <input v-model="form.features" type="checkbox" value="Power outlets">
                  Power outlets
                </label>
                <label>
                  <input v-model="form.features" type="checkbox" value="Quiet seating">
                  Quiet seating
                </label>
              </div>
            </div>
          </div>
        </fieldset>

        <div class="form-actions">
          <button type="submit" class="button button-primary">Submit preferences</button>
        </div>

        <p v-if="successMessage" class="form-success">{{ successMessage }}</p>
      </form>
    </section>
  </main>
</template>
