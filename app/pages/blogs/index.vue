<script setup>
  const { data, error } = await useFetch('https://jsonplaceholder.typicode.com/posts')
</script>

<template>
  <section>
    <h1>Blog Posts</h1>
    <div v-if="error" class="error">
      Unable to load blog posts right now.
    </div>
    <div v-else-if="data" class="blog-grid">
      <article v-for="post in data" :key="post.id" class="blog-card">
        <h2>{{ post.title }}</h2>
        <p class="blog-content">{{ post.body }}</p>
        <NuxtLink :to="`/blogs/${post.id}`">Read more</NuxtLink>
      </article>
    </div>
  </section>
</template>

<style scoped>
  section {
    max-width: 900px;
    margin: 0 auto;
  }
  .blog-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
  }
  .blog-card {
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    padding: 1rem;
  }
  .blog-content{
    max-height: 200px;
    overflow: hidden;
  }
  .error {
    color: #b91c1c;
  }
</style>