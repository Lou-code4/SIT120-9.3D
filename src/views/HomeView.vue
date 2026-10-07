<script setup>
import hotMatchaImage from '../assets/hot-matcha.jpeg'

const emit = defineEmits(['navigate'])
</script>

<template>
  <main>
    <section class="hero">
      <div class="hero-copy">
        <p class="eyebrow">Melbourne matcha guide</p>
        <h2>Find your next matcha cafe without the endless scrolling.</h2>
        <p>
          Compare Melbourne matcha cafe options by location, price, rating and
          practical needs such as studying, meeting friends or grabbing takeaway.
        </p>
        <a class="button button-primary" href="#" @click.prevent="emit('navigate', 'cafes')">Browse Cafes</a>
      </div>

      <figure class="matcha-card">
        <img
          :src="hotMatchaImage"
          alt="Hot matcha latte with latte art held outdoors"
          class="matcha-image"
        >
        <figcaption>
          <p>Featured drink</p>
          <strong>Hot matcha latte</strong>
        </figcaption>
      </figure>
    </section>

    <section class="section-block">
      <p class="eyebrow">Choose with useful details</p>
      <h2>Compare what matters before you visit.</h2>

      <div class="feature-grid">
        <article class="feature-card">
          <span>01</span>
          <h3>Location</h3>
          <p>See the suburb or area first so you can quickly narrow down nearby options.</p>
        </article>

        <article class="feature-card">
          <span>02</span>
          <h3>Price &amp; Rating</h3>
          <p>Compare typical drink prices and customer ratings before choosing a cafe.</p>
        </article>

        <article class="feature-card">
          <span>03</span>
          <h3>Personal Needs</h3>
          <p>Check whether a cafe suits studying, meeting friends, quiet seating or takeaway.</p>
        </article>
      </div>
    </section>
  </main>
</template>
