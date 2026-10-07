<script setup>
import { computed } from 'vue'
import icedMatchaImage from '../assets/iced-matcha.png'
import strawberryMatchaImage from '../assets/matcha.webp'
import hotMatchaImage from '../assets/hot-matcha.jpeg'

const props = defineProps({
  cafeId: {
    type: String,
    default: 'moss'
  }
})

const emit = defineEmits(['navigate'])

const cafes = {
  moss: {
    name: 'Moss & Whisk',
    location: 'CBD',
    price: '$7–$9',
    rating: '4.7',
    image: icedMatchaImage,
    imageAlt: 'Iced matcha drink served in a clear glass',
    hours: '7:30 am–5:00 pm',
    popularDrink: 'Classic iced matcha',
    study: 'Yes, with Wi-Fi and quiet seating',
    meeting: 'Suitable for small groups',
    menu: [
      { price: '$7.00', name: 'Hot Matcha', description: 'Traditional matcha with your choice of milk.' },
      { price: '$7.50', name: 'Iced Matcha', description: 'A chilled matcha latte with light sweetness.' },
      { price: '$8.50', name: 'Strawberry Matcha', description: 'Matcha layered with strawberry and milk.' }
    ]
  },
  green: {
    name: 'Green Hour',
    location: 'Carlton',
    price: '$8–$10',
    rating: '4.5',
    image: strawberryMatchaImage,
    imageAlt: 'Iced strawberry matcha drink',
    hours: '8:00 am–6:00 pm',
    popularDrink: 'Strawberry matcha',
    study: 'Some laptop-friendly seating',
    meeting: 'Yes, social seating for friends',
    menu: [
      { price: '$8.00', name: 'Iced Matcha', description: 'Smooth iced matcha with your choice of milk.' },
      { price: '$9.00', name: 'Strawberry Matcha', description: 'Matcha layered with strawberry and milk.' },
      { price: '$9.50', name: 'Mango Matcha', description: 'Fruit matcha with a bright mango layer.' }
    ]
  },
  quiet: {
    name: 'Quiet Leaf',
    location: 'South Yarra',
    price: '$7–$8',
    rating: '4.6',
    image: hotMatchaImage,
    imageAlt: 'Hot matcha latte with green latte art',
    hours: '7:00 am–4:30 pm',
    popularDrink: 'Traditional hot matcha',
    study: 'Yes, calm seating for quiet work',
    meeting: 'Best for quiet catch-ups',
    menu: [
      { price: '$7.00', name: 'Traditional Matcha', description: 'Whisked matcha served warm and simple.' },
      { price: '$7.50', name: 'Matcha Latte', description: 'Hot matcha finished with steamed milk.' },
      { price: '$8.00', name: 'Iced Matcha', description: 'A chilled version for warmer Melbourne days.' }
    ]
  }
}

const cafe = computed(() => cafes[props.cafeId] || cafes.moss)
</script>

<template>
  <main>
    <section class="page-intro">
      <p class="eyebrow">Cafe details</p>
      <h2>{{ cafe.name }}</h2>
      <p>
        A closer look at this cafe using the practical information planned in
        the original website wireframe.
      </p>
    </section>

    <section class="section-block cafe-detail-layout">
      <div>
        <img :src="cafe.image" :alt="cafe.imageAlt" class="detail-image">
      </div>

      <article class="detail-panel">
        <p class="rating" :aria-label="`Rating ${cafe.rating} out of 5`">★ {{ cafe.rating }} / 5 customer rating</p>
        <h3>{{ cafe.location }} · {{ cafe.price }}</h3>
        <dl class="detail-list">
          <div><dt>Opening hours</dt><dd>{{ cafe.hours }}</dd></div>
          <div><dt>Popular drink</dt><dd>{{ cafe.popularDrink }}</dd></div>
          <div><dt>Study friendly</dt><dd>{{ cafe.study }}</dd></div>
          <div><dt>Meeting friends</dt><dd>{{ cafe.meeting }}</dd></div>
        </dl>
        <a class="button button-primary" href="#" @click.prevent="emit('navigate', 'cafes')">Back to Cafe Guide</a>
      </article>
    </section>

    <section class="section-block">
      <p class="eyebrow">Menu snapshot</p>
      <h2>Popular matcha choices</h2>
      <div class="feature-grid">
        <article v-for="item in cafe.menu" :key="item.name" class="feature-card">
          <span>{{ item.price }}</span>
          <h3>{{ item.name }}</h3>
          <p>{{ item.description }}</p>
        </article>
      </div>
    </section>
  </main>
</template>
