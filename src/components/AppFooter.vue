<script setup>
defineProps({
  activePage: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['navigate'])
</script>

<template>
  <footer class="site-footer">
    <div>
      <p><strong>Matcha Melbourne</strong></p>
      <p>&copy; 2026 Alaa · SIT120 Task 9.3D</p>
      <p>Contact: <a href="mailto:s225563923@deakin.edu.au">s225563923@deakin.edu.au</a></p>
    </div>

    <nav class="footer-nav" aria-label="Secondary navigation">
      <a href="#" :aria-current="activePage === 'home' ? 'page' : undefined" @click.prevent="emit('navigate', 'home')">Home</a>
      <a href="#" :aria-current="activePage === 'cafes' ? 'page' : undefined" @click.prevent="emit('navigate', 'cafes')">Cafes</a>
      <a href="#" :aria-current="activePage === 'details' ? 'page' : undefined" @click.prevent="emit('navigate', 'details')">Cafe Details</a>
      <a href="#" :aria-current="activePage === 'form' ? 'page' : undefined" @click.prevent="emit('navigate', 'form')">Matcha Form</a>
    </nav>
  </footer>
</template>
