<script setup>
defineProps({
  activePage: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['navigate'])

function goTo(page) {
  emit('navigate', page)
}
</script>

<template>
  <header class="site-header">
    <div class="brand">
      <span class="brand-mark" aria-hidden="true">抹</span>
      <div>
        <h1>Matcha Melbourne</h1>
        <p>Find your next green cup in the city.</p>
      </div>
    </div>

    <nav aria-label="Primary navigation">
      <a href="#" :class="{ active: activePage === 'home' }" :aria-current="activePage === 'home' ? 'page' : undefined" @click.prevent="goTo('home')">Home</a>
      <a href="#" :class="{ active: activePage === 'cafes' }" :aria-current="activePage === 'cafes' ? 'page' : undefined" @click.prevent="goTo('cafes')">Cafes</a>
      <a href="#" :class="{ active: activePage === 'details' }" :aria-current="activePage === 'details' ? 'page' : undefined" @click.prevent="goTo('details')">Cafe Details</a>
      <a href="#" :class="{ active: activePage === 'form' }" :aria-current="activePage === 'form' ? 'page' : undefined" @click.prevent="goTo('form')">Matcha Form</a>
    </nav>
  </header>
</template>
