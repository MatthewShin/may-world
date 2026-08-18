<template>
  <div class="about">
    <div class="about-header">
      <h1 class="about-title">About May world</h1>
      <p class="about-subtitle">아름다운 순간들을 담은 포토 갤러리 프로젝트</p>
    </div>

    <div class="about-content">
      <div class="about-section">
        <h2>프로젝트 소개</h2>
        <p>
          이 갤러리는 Vue.js와 TypeScript를 사용하여 제작된 현대적인 포토 갤러리입니다. 아름다운
          순간들을 담은 사진들을 감상할 수 있으며, 반응형 디자인으로 모든 디바이스에서 최적의 경험을
          제공합니다.
        </p>
      </div>

      <div class="about-section">
        <h2>기술 스택</h2>
        <div class="tech-grid">
          <div class="tech-item">
            <div class="tech-icon">⚡</div>
            <h3>Vue.js 3</h3>
            <p>Composition API를 활용한 현대적인 프론트엔드 개발</p>
          </div>
          <div class="tech-item">
            <div class="tech-icon">🔷</div>
            <h3>TypeScript</h3>
            <p>타입 안정성을 보장하는 강력한 개발 환경</p>
          </div>
          <div class="tech-item">
            <div class="tech-icon">🎨</div>
            <h3>CSS3</h3>
            <p>모던한 스타일링과 애니메이션 효과</p>
          </div>
          <div class="tech-item">
            <div class="tech-icon">📱</div>
            <h3>반응형 디자인</h3>
            <p>모든 디바이스에서 최적의 사용자 경험</p>
          </div>
        </div>
      </div>

      <div class="about-section">
        <h2>주요 기능</h2>
        <ul class="features-list">
          <li>🎯 직관적인 네비게이션</li>
          <li>🖼️ 고품질 이미지 갤러리</li>
          <li>📱 모바일 친화적 디자인</li>
          <li>⚡ 빠른 로딩 성능</li>
          <li>🎨 아름다운 UI/UX</li>
        </ul>
      </div>

      <div class="about-section">
        <h2>연락처</h2>
        <div class="contact-info">
          <p><strong>이메일:</strong> reodavin@gmail.com</p>
          <p><strong>전화번호:</strong> 010.3258.6912</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
// About 페이지 로직
</script>

<style scoped>
.about {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

.about-header {
  text-align: center;
  margin-bottom: 3rem;
  padding: 3rem 2rem;
  background: var(--color-dark-canvas);
  color: var(--color-dark-text);
  border-radius: var(--radius-m);
}

.about-title {
  font-family: var(--font-display);
  font-size: 2.4rem;
  font-weight: 600;
  margin-bottom: 0.75rem;
}

.about-subtitle {
  font-size: 1.1rem;
  color: var(--color-dark-muted);
}

.about-content {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.about-section {
  background: var(--color-surface);
  padding: 2rem;
  border-radius: var(--radius-m);
  border: 1px solid var(--color-border);
}

.about-section h2 {
  font-family: var(--font-display);
  color: var(--color-heading);
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  border-bottom: 2px solid var(--color-accent);
  padding-bottom: 0.5rem;
  display: inline-block;
}

.about-section p {
  color: var(--color-muted);
  line-height: 1.8;
  font-size: 1rem;
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.tech-item {
  text-align: center;
  padding: 1.5rem;
  background: var(--color-surface-sunken);
  border-radius: var(--radius-m);
  transition: transform var(--motion-base);
}

.tech-item:hover {
  transform: translateY(-3px);
}

.tech-icon {
  font-size: 2.25rem;
  margin-bottom: 1rem;
}

.tech-item h3 {
  color: var(--color-heading);
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
}

.tech-item p {
  color: var(--color-muted);
  font-size: 0.9rem;
  line-height: 1.5;
}

.features-list {
  list-style: none;
  padding: 0;
}

.features-list li {
  padding: 0.75rem 0;
  border-bottom: 1px solid var(--color-border);
  font-size: 1rem;
  color: var(--color-muted);
}

.features-list li:last-child {
  border-bottom: none;
}

.contact-info {
  background: var(--color-surface-sunken);
  padding: 1.5rem;
  border-radius: var(--radius-m);
}

.contact-info p {
  margin: 0.5rem 0;
  font-size: 1rem;
  color: var(--color-muted);
}

.contact-info strong {
  color: var(--color-heading);
}

@media (max-width: 768px) {
  .about {
    padding: 1rem;
  }

  .about-title {
    font-size: 2rem;
  }

  .tech-grid {
    grid-template-columns: 1fr;
  }

  .about-section {
    padding: 1.5rem;
  }
}
</style>
