<script setup lang="ts">
definePageMeta({
  validate (route) {
    // Check if the id is made up of digits
    return typeof route.params.id === 'string' && /^\d+$/.test(route.params.id)
  },
})

const title = ref('Blog Post')
const content = ref('This is the content of the blog post.')
const cover = 'https://images.unsplash.com/photo-1432821596592-e2c18b78144f?fm=jpg&q=60&w=3000&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxzZWFyY2h8M3x8YmxvZyUyMGNvdmVyfGVufDB8fDB8fHww'
const route = useRoute()
const { data, error } = await useFetch(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
const { data: comments } = await useFetch(`https://jsonplaceholder.typicode.com/posts/${route.params.id}/comments`)

useHead({
  title: title,
  meta: [
    {
      name: 'description',
      content: content,
    },
  ],
})
useSeoMeta({
  title: title,
  ogDescription: content,
  ogImage: cover,
  twitterCard: 'summary_large_image',
})

</script>
<template>
  <section>
    <h1>{{ title }}</h1>
    <div v-if="data" class="blog-detail">
      <img :src="cover" alt="Blog cover" class="cover">
      <h1>{{ data.title }}</h1>
      <p>{{ data.body }}</p>
      <small class="date">20 July 2026</small>
      <div v-if="error">
        <p>Blog post not found.</p>
      </div>
    </div>
  </section>
  <!-- comments -->
  <section>
    <h2>Comments</h2>
    <div v-if="data" class="comments">
      <div v-for="comment in comments" :key="comment.id" class="comment">
        <p>
          <strong>{{ comment.name }} </strong> ({{ comment.email }})</p>
        <p>{{ comment.body }}</p>
        <hr>
      </div>
    </div>
  </section>
</template>

<style scoped>
  section {
    padding: 1rem;
  }
  p {
    margin: 0.5rem 0;
    color: #333;
  }
  .container {
    display: inline-block;
    width: 100%;
  }
  .card {
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    padding: 1rem;
    margin: .5rem;
    padding-top: 0.5rem;
    padding-bottom: 0.5rem;
  }
  .card h3 {
    font-size: 1.25rem;
    font-weight: 600;
  }
  .cover{
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 4px;
    margin-bottom: 1rem;
  }
  .date {
    font-size: 0.875rem;
    color: #6b7280;
  }
</style>