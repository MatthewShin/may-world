<template>
  <div class="golf-course-list">
    <div class="header">
      <h1 class="title">🏌️‍♂️ 멍충이 Golf Course List</h1>
      <p class="subtitle">Discover beautiful golf courses across the country</p>
    </div>

    <div class="filters">
      <div class="filter-container">
        <div class="filter-group">
          <label class="filter-label">Course Difficulty:</label>
          <select
            v-model="selectedCourseDifficulty"
            @change="handleCourseDifficultyFilter"
            class="filter-select"
          >
            <option value="all">All Levels</option>
            <option value="1">🐶 +</option>
            <option value="2">🐶🐶 +</option>
            <option value="3">🐶🐶🐶 +</option>
            <option value="4">🐶🐶🐶🐶 +</option>
            <option value="5">🐶🐶🐶🐶🐶</option>
          </select>
        </div>

        <div class="filter-group">
          <label class="filter-label">Green Difficulty:</label>
          <select
            v-model="selectedGreenDifficulty"
            @change="handleGreenDifficultyFilter"
            class="filter-select"
          >
            <option value="all">All Levels</option>
            <option value="1">🐰 +</option>
            <option value="2">🐰🐰 +</option>
            <option value="3">🐰🐰🐰 +</option>
            <option value="4">🐰🐰🐰🐰 +</option>
            <option value="5">🐰🐰🐰🐰🐰</option>
          </select>
        </div>
      </div>

      <div class="reset-container">
        <button
          @click="handleResetFilters"
          class="reset-btn"
          :class="{ active: isAnyFilterActive }"
        >
          🔄 Reset Filters
        </button>
      </div>
    </div>

    <div class="course-list">
      <div
        v-for="course in filteredCourses"
        :key="course.id"
        class="course-item"
        @click="handleCourseClick(course)"
      >
        <div class="course-image">
          <div class="image-placeholder">{{ getRandomEmoji(course.id) }}</div>
        </div>
        <div class="course-info">
          <h3 class="course-name">{{ course.name }}</h3>
          <div class="course-location">📍 {{ course.location }}</div>
          <div class="course-stats">
            <div class="stat-item">
              <span class="stat-label">Course Difficulty:</span>
              <div class="stars">
                <span
                  v-for="i in 5"
                  :key="i"
                  class="star"
                  :class="{ filled: i <= course.courseDifficulty }"
                >
                  🐶
                </span>
              </div>
            </div>
            <div class="stat-item">
              <span class="stat-label">Green Difficulty:</span>
              <div class="stars">
                <span
                  v-for="i in 5"
                  :key="i"
                  class="star"
                  :class="{ filled: i <= course.greenDifficulty }"
                >
                  🐰
                </span>
              </div>
            </div>
            <div class="stat-item">
              <span class="stat-label">Total Length:</span>
              <span class="stat-value">{{ course.totalLength }}m</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div v-if="filteredCourses.length === 0" class="no-results">
      <p>No results found.</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { golfCourses, getRandomEmoji, type GolfCourse } from '../data/golfCourses';

const selectedCourseDifficulty = ref('all');
const selectedGreenDifficulty = ref('all');

const filteredCourses = computed(() => {
  let filtered = golfCourses;

  if (selectedCourseDifficulty.value !== 'all') {
    const minCourseDifficulty = parseInt(selectedCourseDifficulty.value);
    filtered = filtered.filter((course) => course.courseDifficulty >= minCourseDifficulty);
  }

  if (selectedGreenDifficulty.value !== 'all') {
    const minGreenDifficulty = parseInt(selectedGreenDifficulty.value);
    filtered = filtered.filter((course) => course.greenDifficulty >= minGreenDifficulty);
  }

  // 정렬 로직
  const isCourseFiltered = selectedCourseDifficulty.value !== 'all';
  const isGreenFiltered = selectedGreenDifficulty.value !== 'all';

  if (isCourseFiltered && !isGreenFiltered) {
    // 코스 난이도만 선택된 경우: 코스 난이도 오름차순
    filtered = filtered.sort((a, b) => a.courseDifficulty - b.courseDifficulty);
  } else if (!isCourseFiltered && isGreenFiltered) {
    // 그린 난이도만 선택된 경우: 그린 난이도 오름차순
    filtered = filtered.sort((a, b) => a.greenDifficulty - b.greenDifficulty);
  } else if (isCourseFiltered && isGreenFiltered) {
    // 둘 다 선택된 경우: 코스 난이도 기준 오름차순
    filtered = filtered.sort((a, b) => a.courseDifficulty - b.courseDifficulty);
  }

  return filtered;
});

const handleCourseDifficultyFilter = () => {
  // 필터링은 computed에서 자동으로 처리됨
};

const handleGreenDifficultyFilter = () => {
  // 필터링은 computed에서 자동으로 처리됨
};

const isAnyFilterActive = computed(() => {
  return selectedCourseDifficulty.value !== 'all' || selectedGreenDifficulty.value !== 'all';
});

const handleResetFilters = () => {
  selectedCourseDifficulty.value = 'all';
  selectedGreenDifficulty.value = 'all';
};

const handleCourseClick = (course: GolfCourse) => {
  console.log('Selected golf course:', course);
  alert(`You selected ${course.name}!`);
};
</script>

<style scoped>
.golf-course-list {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  min-height: 100vh;
}

.header {
  text-align: center;
  margin-bottom: 3rem;
}

.title {
  font-family: var(--font-display);
  font-size: 2.2rem;
  color: var(--color-heading);
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.subtitle {
  font-size: 1rem;
  color: var(--color-muted);
}

.filters {
  margin-bottom: 2rem;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.filter-container {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.filter-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  min-width: 200px;
}

.filter-label {
  font-weight: 600;
  color: var(--color-muted);
  font-size: 0.8rem;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  text-align: center;
}

.filter-select {
  padding: 0.65rem 1rem;
  border: 1px solid var(--color-border-strong);
  background: var(--color-surface);
  color: var(--color-ink);
  border-radius: var(--radius-s);
  cursor: pointer;
  transition: border-color var(--motion-fast);
  font-weight: 500;
  font-size: 0.9rem;
  outline: none;
}

.filter-select:hover {
  border-color: var(--color-ink);
}

.filter-select:focus-visible {
  border-color: var(--color-accent);
  outline: 2px solid var(--color-accent);
  outline-offset: 1px;
}

.reset-container {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.reset-btn {
  padding: 0.65rem 1.4rem;
  border: 1px solid var(--color-border-strong);
  background: var(--color-surface);
  color: var(--color-muted);
  border-radius: var(--radius-pill);
  cursor: pointer;
  transition: all var(--motion-fast);
  font-weight: 600;
  font-size: 0.85rem;
  outline: none;
}

.reset-btn:hover {
  border-color: var(--color-ink);
  color: var(--color-ink);
}

.reset-btn.active {
  border-color: var(--color-accent);
  color: var(--color-accent-ink);
  background-color: rgba(169, 117, 36, 0.1);
}

.reset-btn.active:hover {
  background-color: var(--color-accent);
  color: var(--color-dark-canvas);
}

.course-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.course-item {
  background: var(--color-surface);
  border-radius: var(--radius-m);
  border: 1px solid var(--color-border);
  overflow: hidden;
  transition:
    transform var(--motion-base),
    border-color var(--motion-base);
  cursor: pointer;
  display: flex;
  height: 140px;
}

.course-item:hover {
  transform: translateY(-3px);
  border-color: var(--color-border-strong);
}

.course-image {
  width: 140px;
  height: 140px;
  background: var(--color-dark-canvas);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.image-placeholder {
  font-size: 2.75rem;
}

.course-info {
  padding: 1.2rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background: var(--color-surface);
}

.course-name {
  font-size: 1.1rem;
  color: var(--color-heading);
  margin-bottom: 0.5rem;
  font-weight: 700;
}

.course-location {
  color: var(--color-muted);
  margin-bottom: 1rem;
  font-size: 0.85rem;
}

.course-stats {
  display: flex;
  gap: 2rem;
  align-items: center;
  flex-wrap: wrap;
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  min-width: 120px;
}

.stat-label {
  font-weight: 600;
  color: var(--color-muted);
  font-size: 0.8rem;
  white-space: nowrap;
}

.stars {
  display: flex;
  gap: 0.2rem;
}

.star {
  font-size: 0.8rem;
  opacity: 0.35;
  transition: all var(--motion-fast);
  filter: grayscale(1);
}

.star.filled {
  opacity: 1;
  transform: scale(1.1);
  filter: grayscale(0) sepia(1) saturate(3) hue-rotate(-10deg);
}

.stat-value {
  font-weight: 700;
  color: var(--color-ink);
  font-size: 0.9rem;
  font-variant-numeric: tabular-nums;
}

.no-results {
  text-align: center;
  padding: 3rem;
  color: var(--color-muted);
  font-size: 1.1rem;
  background: var(--color-surface);
  border-radius: var(--radius-m);
  border: 1px solid var(--color-border);
}

@media (max-width: 770px) {
  .golf-course-list {
    padding: 1rem;
  }

  .title {
    font-size: 1.9rem;
  }

  .filter-container {
    flex-direction: column;
    align-items: center;
    gap: 1rem;
  }

  .filter-group {
    width: 100%;
    max-width: 300px;
  }

  .course-item {
    height: auto;
    min-height: 120px;
    flex-direction: column;
  }

  .course-image {
    width: 100%;
    height: 120px;
  }

  .image-placeholder {
    font-size: 2.5rem;
  }

  .course-info {
    padding: 1rem;
    width: 100%;
  }

  .course-stats {
    flex-direction: column;
    gap: 0.5rem;
    align-items: flex-start;
    width: 100%;
  }

  .stat-item {
    min-width: auto;
    width: 100%;
    justify-content: space-between;
  }

  .stat-label {
    font-size: 0.8rem;
  }

  .stars {
    flex-wrap: wrap;
  }

  .star {
    font-size: 0.7rem;
  }

  .stat-value {
    font-size: 0.8rem;
  }
}
</style>
