<script setup lang="ts">
definePageMeta({
  validate(route) {
    return typeof route.params.id === 'string' && /^\d+$/.test(route.params.id)
  },
})

const route = useRoute()
const { data: product, error } = await useFetch(`https://fakestoreapi.com/products/${route.params.id}`)
const cover = ref('https://wildromanticphotography.com/wp-content/uploads/How-to-Photograph-Flat-Lay-Clothing-3.jpg');
useHead({
  title: computed(() => product.value?.title || 'Product Details'),
})
</script>

<template>
  <section>
    <img :src="cover" class="cover" alt="Product Cover" />
    <div v-if="error || !product" class="error">
      Product not found.
    </div>

    <div v-else class="product-detail">
      <img :src="product.image" :alt="product.title" />
      <div>
        <h1>{{ product.title }}</h1>
        <p class="price">${{ product.price }}</p>
        <p>{{ product.description }}</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
section {
  max-width: 900px;
  margin: 0 auto;
}
.cover{
  width: 100%;
  max-height: 400px;
  object-fit: cover;
  margin-bottom: 4rem;
}
.product-detail {
  display: grid;
  grid-template-columns: 280px 1fr;
  gap: 2rem;
  align-items: start;
}
.product-detail img {
  width: 100%;
  max-height: 320px;
  object-fit: contain;
}
.price {
  font-size: 1.25rem;
  font-weight: 700;
  color: #059669;
}
.error {
  color: #b91c1c;
}
</style>