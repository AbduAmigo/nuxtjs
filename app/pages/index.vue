<script setup lang="ts">
const title = ref('Home Page')
const description = ref('Welcome to our Nuxt 3 application!')
const intro = ref('https://images.unsplash.com/photo-1432821596592-e2c18b78144f?fm=jpg&q=100&w=3000')
const { data, error } = await useFetch('https://fakestoreapi.com/products')

const client_logos = {
  1: 'https://logomakerr.ai/blog/wp-content/uploads/2022/08/2019-to-Present-Zara-logo-design.jpg',
  2: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgdnoLke6rQ84R9NT-NXzwU9II5phGrE_v-ntImxNAPw&s=10',
  3: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRvyWLib1nfcVYfki7iJylDC-6tRrS30elWcAR_qfYOqA&s=10'
}
const { data: clients, error: clientsError } = await useFetch('https://jsonplaceholder.typicode.com/photos')

useHead({
  title,
  meta: [
    {
      name: 'description',
      content: description,
    },
  ],
})

useSeoMeta({
  title,
  ogDescription: description,
  ogImage: intro,
  twitterCard: 'summary_large_image',
})
</script>

<template>
  <!-- intro -->
  <section class="section home-page">
    <div class="intro-image">
      <img :src="intro" alt="Intro Image" />
    </div>
    <div class="caption">
      <h1>Welcome to Mini Shop</h1>
      <p>Find the latest products and learn more about us.</p>
      <a class="get-started" href="/products">Get Started</a>
    </div>
  </section>

  <!-- products -->
  <section class="section product-page" id="products">
    <h1 class="product-title">Featured Products</h1>
    <p>Check out our latest products below.</p>
    <div v-if="error" class="error">
      Unable to load products right now.
    </div>
    <div v-else-if="data" class="product-grid">
      <article v-for="product in data.slice(0, 4)" :key="product.id" class="product-card">
        <div class="img-item">
          <img :src="product.image" :alt="product.title" />
        </div>
        <h2>{{ product.title }}</h2>
        <p class="price">${{ product.price }}</p>
        <NuxtLink :to="`/products/${product.id}`">View details</NuxtLink>
      </article>
    </div>
    <div class="center">
        <NuxtLink class="view-all" href="/products">View All Products</NuxtLink>
    </div>
  </section>

  <!-- video section -->
  <section class="section video-section">
    <iframe width="100%" height="400" src="https://www.youtube.com/embed/gbLmku5QACM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
  </section>

  <!-- clients section -->
  <section class="section clients-section">
    <h2>Our Clients</h2>
    <div v-if="clientsError" class="error">
      Unable to load clients right now.
    </div>
    <div v-else-if="clients" class="clients-grid">
      <article v-for="client in clients.slice(0, 3)" :key="client.id" class="client-card">
        <img :src="client_logos[client.id] ?? 'https://cdn.vectorstock.com/i/1000v/43/94/grey-profile-icon-avatar-placeholder-vector-38594394.jpg'" :alt="client.title" />
      </article>
    </div>
  </section>
</template>

<style scoped>
section {
  max-width: 1100px;
  margin: 5px auto;
}
.section {
  margin-top: 0.4rem;
  margin-bottom: 8rem;
}
.home-page {
  line-height: 1.6;
  background-color: #1b3d5f;
}
.intro-image {
  width: 100%;
  max-height: 400px;
  object-fit: cover;
  margin-bottom: 1rem;
  opacity: 0.8;
}
.caption{
  position: absolute;
  top: 10rem;
  margin: 5rem
}
.caption h1 {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #fff;
}
.caption p {
  font-size: 1rem;
  background-color: #fff;
  color: #797676;
  padding: 0.5rem;
  border-radius: 4px;
}
.get-started {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background-color: #059669;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
}
.get-started:hover {
  background-color: #047857;
}
.intro-image img {
  width: 100%;
  height: 400px;
  object-fit: cover;
}
/* products */
.product-page h1{
  justify-content: center;
  text-align: center;
  font-size: 2rem;
  margin-bottom: 0.5rem;
}
.product-page p{
  justify-content: center;
  text-align: center;
  font-size: 1.25rem;
  margin-bottom: 1rem;
}
.center {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}
.view-all {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background-color: #059669;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  text-align: center;
}
.view-all:hover {
  background-color: #047857;
}
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}
.product-card {
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 1rem;
}
.product-card h2 {
  font-size: 1rem;
  margin-bottom: 0.5rem;
  max-height: 2.5rem;
  overflow: hidden;
  height: 2.5rem;
}
.product-card img {
  width: 100%;
  height: 180px;
  object-fit: contain;
  margin-bottom: 0.75rem;
}
.img-item {
  width: 100%;
  height: 180px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #6363901c;
}
.price {
  font-weight: 600;
  color: #059669;
}
.error {
  color: #b91c1c;
}
/* video section */
.video-section {
  margin-top: 2rem;
  text-align: center;
  width: 80%
}
/* clients section */
.clients-section {
  margin-top: 2rem;
}
.clients-section h2 {
  justify-content: center;
  text-align: center;
  font-size: 2rem;
  margin-bottom: 0.5rem;
}
.clients-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}
.client-card {
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 1rem;
}
.client-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}
</style>