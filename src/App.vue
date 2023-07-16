<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router'

const routes = useRouter().getRoutes()
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <router-link v-for="route in routes" :key="route.path" :to="route.path">
          {{ route.name }} |
        </router-link>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}
</style>
