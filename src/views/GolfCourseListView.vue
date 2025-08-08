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
  background-color: #f8f9fa;
  min-height: 100vh;
}

.header {
  text-align: center;
  margin-bottom: 3rem;
}

.title {
  font-size: 2.4rem;
  color: #1a1a1a;
  margin-bottom: 0.5rem;
  font-weight: 900;
}

.subtitle {
  font-size: 1.1rem;
  color: #666;
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
  color: #333;
  font-size: 0.9rem;
  text-align: center;
}

.filter-select {
  padding: 0.75rem 1rem;
  border: 2px solid #333;
  background: white;
  color: #333;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 500;
  font-size: 0.9rem;
  outline: none;
}

.filter-select:hover {
  border-color: #666;
}

.filter-select:focus {
  border-color: #333;
  background-color: #f8f9fa;
}

.reset-container {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.reset-btn {
  padding: 0.75rem 1.5rem;
  border: 2px solid #ccc;
  background: white;
  color: #666;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  font-weight: 600;
  font-size: 0.9rem;
  outline: none;
}

.reset-btn:hover {
  border-color: #333;
  color: #333;
  transform: translateY(-2px);
}

.reset-btn.active {
  border-color: #e74c3c;
  color: #e74c3c;
  background-color: #fff5f5;
}

.reset-btn.active:hover {
  background-color: #e74c3c;
  color: white;
}

.course-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.course-item {
  background: white;
  border-radius: 1rem;
  border: 1px solid #e0e0e0;
  overflow: hidden;
  transition: transform 0.3s ease;
  cursor: pointer;
  display: flex;
  height: 140px;
}

.course-item:hover {
  transform: translateY(-3px);
}

.course-image {
  width: 140px;
  height: 140px;
  background: linear-gradient(135deg, #2c2c2c 0%, #4a4a4a 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

.image-placeholder {
  font-size: 3rem;
  color: white;
  filter: grayscale(0.3);
}

.course-info {
  padding: 1.2rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  background: white;
}

.course-name {
  font-size: 1.2rem;
  color: #1a1a1a;
  margin-bottom: 0.5rem;
  font-weight: 700;
}

.course-location {
  color: #666;
  margin-bottom: 1rem;
  font-size: 0.9rem;
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
  color: #333;
  font-size: 0.85rem;
  white-space: nowrap;
}

.stars {
  display: flex;
  gap: 0.2rem;
}

.star {
  font-size: 0.8rem;
  opacity: 0.2;
  transition: all 0.3s ease;
  color: #ccc;
  filter: grayscale(1);
}

.star.filled {
  opacity: 1;
  color: #e74c3c;
  transform: scale(1.1);
  filter: grayscale(0);
}

.stat-value {
  font-weight: 700;
  color: #333;
  font-size: 0.9rem;
}

.no-results {
  text-align: center;
  padding: 3rem;
  color: #666;
  font-size: 1.1rem;
  background: white;
  border-radius: 1rem;
  border: 1px solid #e0e0e0;
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
