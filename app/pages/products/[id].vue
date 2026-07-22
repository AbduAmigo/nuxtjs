<script setup lang="ts">
definePageMeta({
  validate(route) {
    return typeof route.params.id === 'string' && /^\d+$/.test(route.params.id)
  },
})

const route = useRoute()
const { data: product, error } = await useFetch(`https://fakestoreapi.com/products/${route.params.id}`)
const { data: reviews, error: reviewError } = await useFetch(`https://fakeapi.net/reviews`)
const cover = ref('https://wildromanticphotography.com/wp-content/uploads/How-to-Photograph-Flat-Lay-Clothing-3.jpg')

useHead({
  title: computed(() => product.value?.title || 'Product Details'),
})
const fetchReviews = async (page: number) => {
  if (!page) return
  const { data, error } = await useFetch(`https://fakeapi.net/reviews?page=${page}`)
  if (error.value) {
    console.error('Error fetching reviews:', error.value)
    return
  }
  reviews.value = data.value
}
const total = reviews.value.pagination.total;
const limit = reviews.value.pagination.limit;

const totalPages = computed(() => {
  if (!total || !limit) return 0
  return Math.ceil(total / limit)
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
  <hr>
  
  <section class="reviews-section">
    <h2>Reviews</h2>
    <div class="reviews-container">
      <!-- reviews -->
      <div v-for="review in reviews?.data" :key="review.id" class="review">
        <h3>{{review.title}}</h3>
        <p>{{review.content}}</p>
        <p>Rating: {{review.rating}}/5</p>
      </div>
      <!-- pagination -->
      <div>
        <span>
          <button class="pagination-button" v-for="page in totalPages" :key="page" @click="fetchReviews(page)">{{ page }}</button>
        </span>
      </div>
    </div>
  </section>
</template>

<style scoped>
  section {
    max-width: 900px;
    margin: 0 auto;
  }
  .reviews-section {
    margin-top: 4rem;
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
  .review {
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    padding: 1rem;
    margin-bottom: 1rem;
    width: 50%;
  }
  .reviews-container {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .pagination-button {
    background-color: #f3f4f6;
    border: 1px solid #d1d5db;
    border-radius: 4px;
    padding: 0.5rem 1rem;
    margin-right: 0.5rem;
    cursor: pointer;
  }
  .pagination-button:hover {
    background-color: #e5e7eb;
  }
</style>