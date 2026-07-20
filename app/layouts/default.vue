<template>
  <div class="app-shell">
    <header class="top-nav">
      <a href="/" class="logo">Mini Shop</a>
      <nav>
        <NuxtLink to="/">Home</NuxtLink>
        <NuxtLink to="/about">About</NuxtLink>
        <NuxtLink to="/products">Products</NuxtLink>
        <NuxtLink to="/blogs">Blogs</NuxtLink>
      </nav>
    </header>

    <main class="page-content">
      <slot />
    </main>

    <footer class="page-footer">
      <p>© 2026 Mini Shop</p>
    </footer>
  </div>
</template>

<style scoped>
.app-shell {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.top-nav {
  background: #1f2937;
  padding: 1rem 1.5rem;
  display: flex;
  align-items: center;
}
.top-nav nav {
  display: flex;
  gap: 1rem;
}
.top-nav a {
  color: #fff;
  text-decoration: none;
}
.top-nav a:hover {
  text-decoration: underline;
}
.logo{
  font-weight: bold;
  color: #fff;
  text-decoration: none;
  margin-right: 40rem;
}
.page-content {
  flex: 1;
  padding: 1.5rem;
}
.page-footer {
  background: #f3f4f6;
  padding: 1rem 1.5rem;
  text-align: center;
  color: #4b5563;
}
</style>
  