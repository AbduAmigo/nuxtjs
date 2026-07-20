<script setup lang="ts">
const { data: teams, error: teamsError } = await useFetch('https://jsonplaceholder.typicode.com/users') 
const team_profile = {
  1: 'https://cdn.vectorstock.com/i/1000v/46/76/gray-male-head-placeholder-vector-23804676.jpg',
  2: 'https://cdn.vectorstock.com/i/1000v/43/94/grey-profile-icon-avatar-placeholder-vector-38594394.jpg',
  3: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTLjTDvHm8KgXlB8WdsPmMlCFUaqKrkoQ_jGyusTmex-w&s=10',
  4: 'https://cdn.vectorstock.com/i/1000x1000/46/76/gray-male-head-placeholder-vector-23804676.jpg',
  5: 'https://cdn.vectorstock.com/i/1000x1000/43/94/grey-profile-icon-avatar-placeholder-vector-38594394.jpg',
  6: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTLjTDvHm8KgXlB8WdsPmMlCFUaqKrkoQ_jGyusTmex-w&s=10',
  7: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTZ227dzyaLmO5mKDUTA8bCBZX2S2lqiK5X-KpSpAZLXQ&s=10'
}
</script>

<template>
  <section>
    <h1>About Us</h1>
    <p>We help customers discover quality products with a seamless shopping experience.</p>
    <p>This page is now wired to the /about route and renders correctly through Nuxt.</p>
  </section>
    <!-- teams section -->
  <section class="section teams-section">
    <h2>Our Team</h2>
    <div v-if="teamsError" class="error">
      Unable to load team members right now.
    </div>
    <div v-else-if="teams" class="teams-grid">
      <article v-for="team in teams" :key="team.id" class="team-card">
        <img :src="team_profile[team.id] ?? 'https://cdn.vectorstock.com/i/1000v/43/94/grey-profile-icon-avatar-placeholder-vector-38594394.jpg'" :alt="team.name" />
        <h3>{{ team.name }}</h3>
        <p><a :href="`mailto:${team.email}`">{{ team.email }}</a></p>
        <span>
          <p>{{ team.address.city }}</p>
          <p>{{ team.address.street }}</p>
        </span>
      </article>
    </div>
  </section>
</template>

<style scoped>
section {
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.6;
}
h1 {
  margin-bottom: 0.75rem;
}
/* teams section */
.teams-section {
  margin-top: 2rem;
}
.teams-section h2 {
  justify-content: center;
  text-align: center;
  font-size: 2rem;
  margin-bottom: 0.5rem;
}
.teams-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}
.team-card {
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 1rem;
}
.team-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  margin-bottom: 0.75rem;
}
</style>
