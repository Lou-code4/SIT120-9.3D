<script setup>
import icedMatchaImage from '../assets/iced-matcha.png'
import strawberryMatchaImage from '../assets/matcha.webp'
import hotMatchaImage from '../assets/hot-matcha.jpeg'

const emit = defineEmits(['navigate', 'select-cafe'])
</script>

<template>
  <main>
    <section class="page-intro">
      <p class="eyebrow">Cafe guide</p>
      <h2>Compare cafes before choosing your next stop.</h2>
      <p>
        Use location, typical price, rating and visit needs to compare these
        example Melbourne matcha cafes. The information is grouped consistently
        so it can be scanned quickly on mobile and desktop.
      </p>
    </section>

    <section class="cafe-grid" aria-label="Matcha cafe recommendations">
      <article class="cafe-card">
        <img :src="icedMatchaImage" alt="Iced matcha drink in a clear glass" class="cafe-image">
        <div class="cafe-tag">CBD</div>
        <h3>Moss &amp; Whisk</h3>
        <p class="rating" aria-label="Rating 4.7 out of 5">★ 4.7 / 5</p>
        <dl class="cafe-facts">
          <div><dt>Price</dt><dd>$7–$9</dd></div>
          <div><dt>Best for</dt><dd>Study sessions</dd></div>
          <div><dt>Features</dt><dd>Wi-Fi, quiet seating</dd></div>
        </dl>
        <a class="text-cta" href="#" @click.prevent="emit('select-cafe', 'moss')">View cafe details</a>
      </article>

      <article class="cafe-card">
        <img :src="strawberryMatchaImage" alt="Iced strawberry matcha drink" class="cafe-image">
        <div class="cafe-tag">Carlton</div>
        <h3>Green Hour</h3>
        <p class="rating" aria-label="Rating 4.5 out of 5">★ 4.5 / 5</p>
        <dl class="cafe-facts">
          <div><dt>Price</dt><dd>$8–$10</dd></div>
          <div><dt>Best for</dt><dd>Meeting friends</dd></div>
          <div><dt>Features</dt><dd>Fruit matcha, social seating</dd></div>
        </dl>
        <a class="text-cta" href="#" @click.prevent="emit('select-cafe', 'green')">View cafe details</a>
      </article>

      <article class="cafe-card">
        <img :src="hotMatchaImage" alt="Hot matcha latte with green latte art" class="cafe-image">
        <div class="cafe-tag">South Yarra</div>
        <h3>Quiet Leaf</h3>
        <p class="rating" aria-label="Rating 4.6 out of 5">★ 4.6 / 5</p>
        <dl class="cafe-facts">
          <div><dt>Price</dt><dd>$7–$8</dd></div>
          <div><dt>Best for</dt><dd>Quiet mornings</dd></div>
          <div><dt>Features</dt><dd>Traditional matcha, calm seating</dd></div>
        </dl>
        <a class="text-cta" href="#" @click.prevent="emit('select-cafe', 'quiet')">View cafe details</a>
      </article>
    </section>

    <section class="section-block">
      <p class="eyebrow">Quick comparison</p>
      <h2>Compare the key selection criteria.</h2>
      <p class="table-intro">
        The table keeps the planned location, price, rating and personal-use information together.
        On smaller screens, swipe horizontally to view every column.
      </p>

      <div class="table-wrap" tabindex="0" aria-label="Scrollable matcha cafe comparison table">
        <table>
          <caption>Example Melbourne matcha cafe comparison</caption>
          <thead>
            <tr>
              <th scope="col">Cafe</th>
              <th scope="col">Location</th>
              <th scope="col">Price</th>
              <th scope="col">Rating</th>
              <th scope="col">Best for</th>
            </tr>
          </thead>
          <tbody>
            <tr><td>Moss &amp; Whisk</td><td>CBD</td><td>$7–$9</td><td>4.7 / 5</td><td>Study sessions</td></tr>
            <tr><td>Green Hour</td><td>Carlton</td><td>$8–$10</td><td>4.5 / 5</td><td>Meeting friends</td></tr>
            <tr><td>Quiet Leaf</td><td>South Yarra</td><td>$7–$8</td><td>4.6 / 5</td><td>Quiet mornings</td></tr>
          </tbody>
        </table>
      </div>
    </section>
  </main>
</template>
