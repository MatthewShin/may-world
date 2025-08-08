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
  padding: 4rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 0 0 2rem 2rem;
  margin-bottom: 3rem;
}

.hero-title {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.hero-subtitle {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  opacity: 0.9;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  display: inline-block;
}

.btn-primary {
  background-color: #42b883;
  color: white;
}

.btn-primary:hover {
  background-color: #369870;
  transform: translateY(-2px);
}

.btn-secondary {
  background-color: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary:hover {
  background-color: white;
  color: #667eea;
  transform: translateY(-2px);
}

.features-section {
  padding: 3rem 2rem;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  color: #2c3e50;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  max-width: 1000px;
  margin: 0 auto;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 1rem;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-5px);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #2c3e50;
}

.feature-card p {
  color: #666;
  line-height: 1.6;
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
