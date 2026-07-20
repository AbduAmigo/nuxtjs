<script setup lang="ts">
const { data, error } = await useFetch('https://fakestoreapi.com/products')
</script>

<template>
  <section>
    <h1>Products</h1>
    <p>Browse our featured products below.</p>

    <div v-if="error" class="error">
      Unable to load products right now.
    </div>

    <div v-else-if="data" class="product-grid">
      <article v-for="product in data" :key="product.id" class="product-card">
        <img :src="product.image" :alt="product.title" />
        <h2>{{ product.title }}</h2>
        <p class="price">${{ product.price }}</p>
        <NuxtLink :to="`/products/${product.id}`">View details</NuxtLink>
      </article>
    </div>
  </section>
</template>

<style scoped>
section {
  max-width: 1100px;
  margin: 0 auto;
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
.product-card img {
  width: 100%;
  height: 180px;
  object-fit: contain;
  margin-bottom: 0.75rem;
}
.price {
  font-weight: 600;
  color: #059669;
}
.error {
  color: #b91c1c;
}
</style>
