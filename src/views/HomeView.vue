<script setup lang="ts">
// 홈페이지 로직
</script>

<template>
  <div class="home">
    <div class="hero-section">
      <h1 class="hero-title">Welcome to May world</h1>
      <p class="hero-subtitle">아름다운 순간들을 담은 포토 갤러리에 오신 것을 환영합니다</p>
      <div class="hero-buttons">
        <router-link to="/gallery" class="btn btn-primary"> 갤러리 보기 </router-link>
        <router-link to="/about" class="btn btn-secondary"> 소개 보기 </router-link>
      </div>
    </div>

    <div class="features-section">
      <h2 class="section-title">특별한 기능들</h2>
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">📸</div>
          <h3>고품질 이미지</h3>
          <p>최고 품질의 사진들을 감상하세요</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🎨</div>
          <h3>아름다운 디자인</h3>
          <p>세련된 UI로 최고의 경험을 제공합니다</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">⚡</div>
          <h3>빠른 로딩</h3>
          <p>최적화된 성능으로 빠른 로딩을 경험하세요</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home {
  min-height: 100vh;
}

.hero-section {
  text-align: center;
  padding: 5rem 2rem;
  background: var(--color-dark-canvas);
  color: var(--color-dark-text);
  border-radius: 0 0 var(--radius-m) var(--radius-m);
  margin-bottom: 3rem;
}

.hero-title {
  font-family: var(--font-display);
  font-size: clamp(2.25rem, 4vw, 3.4rem);
  font-weight: 600;
  line-height: 1.08;
  margin-bottom: 1rem;
  text-wrap: balance;
}

.hero-subtitle {
  font-size: 1.1rem;
  margin-bottom: 2rem;
  color: var(--color-dark-muted);
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  padding: 0.75rem 1.5rem;
  border-radius: var(--radius-s);
  text-decoration: none;
  font-weight: 600;
  font-size: 0.95rem;
  transition: all var(--motion-base);
  display: inline-block;
}

.btn-primary {
  background-color: var(--color-dark-text);
  color: var(--color-dark-canvas);
}

.btn-primary:hover {
  background-color: var(--color-accent);
  color: var(--color-dark-canvas);
}

.btn-secondary {
  background-color: transparent;
  color: var(--color-dark-text);
  border: 1px solid var(--color-dark-muted);
}

.btn-secondary:hover {
  border-color: var(--color-dark-text);
}

.features-section {
  padding: 3rem 2rem;
}

.section-title {
  text-align: center;
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 600;
  margin-bottom: 3rem;
  color: var(--color-heading);
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  max-width: 1000px;
  margin: 0 auto;
}

.feature-card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  padding: 2rem;
  border-radius: var(--radius-m);
  text-align: center;
  transition: transform var(--motion-base);
}

.feature-card:hover {
  transform: translateY(-3px);
  border-color: var(--color-border-strong);
}

.feature-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: var(--color-heading);
}

.feature-card p {
  color: var(--color-muted);
  line-height: 1.6;
  font-size: 0.9rem;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }

  .btn {
    width: 200px;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }
}
</style>
