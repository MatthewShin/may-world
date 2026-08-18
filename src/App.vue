<template>
  <div id="app">
    <nav class="navbar">
      <div class="nav-container">
        <router-link to="/" class="nav-brand">Playground</router-link>
        <div class="nav-links">
          <router-link to="/" class="nav-link">Home</router-link>
          <router-link to="/gallery" class="nav-link">Gallery</router-link>
          <router-link to="/golf-courses" class="nav-link">Golf Courses</router-link>
          <router-link to="/about" class="nav-link">About</router-link>
        </div>
      </div>
    </nav>

    <main class="main-content">
      <router-view />
    </main>
  </div>
</template>

<script setup lang="ts">
// 컴포넌트 로직이 필요하면 여기에 추가
</script>

<style scoped>
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.navbar {
  background-color: var(--color-ink);
  padding: 1rem 0;
  position: sticky;
  top: 0;
  z-index: 1000;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  color: var(--color-dark-text);
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 600;
  text-decoration: none;
  transition: color var(--motion-fast);
}

.nav-brand:hover {
  color: var(--color-accent);
}

.nav-links {
  display: flex;
  gap: 0.5rem;
}

.nav-link {
  color: rgba(242, 240, 234, 0.75);
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  transition: color var(--motion-fast);
  padding: 0.5rem 0.9rem;
  border-radius: var(--radius-s);
}

.nav-link:hover {
  color: var(--color-dark-text);
}

.nav-link.router-link-active {
  color: var(--color-dark-text);
  position: relative;
}

.nav-link.router-link-active::after {
  content: '';
  position: absolute;
  left: 0.9rem;
  right: 0.9rem;
  bottom: 0.15rem;
  height: 2px;
  background: var(--color-accent);
}

.main-content {
  flex: 1;
  padding: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

@media (max-width: 768px) {
  .nav-container {
    flex-direction: column;
    gap: 1rem;
  }

  .nav-links {
    gap: 1rem;
  }

  .main-content {
    padding: 1rem;
  }
}
</style>
