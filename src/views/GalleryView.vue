<template>
  <swiper>
    <swiper-slide v-for="(item, index) in contents" :key="index">
      <div class="container">
        <div class="info theme_2">
          <h2 class="info__title">" {{ item.title.toUpperCase() }} "</h2>
          <p class="info__spot">{{ item.spot }}</p>
          <p class="info__date">{{ item.date }}</p>
        </div>
        <div class="bg">
          <div class="bg__vignette"></div>
          <div id="bg-image" class="bg__image" :style="`background-image: url(${item.src})`"></div>
        </div>
      </div>
    </swiper-slide>
  </swiper>
  <p class="copyright">reodavin@gmail.com / 010.3258.6912</p>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

import 'swiper/css';
import 'swiper/css/pagination';
import { Swiper, SwiperSlide } from 'vue-awesome-swiper';

type Content = {
  title: string;
  spot: string;
  date: string;
  type: 'image' | 'video';
  src: string;
};

type Contents = Array<Content>;

const defaultContents: Contents = [
  {
    title: 'Early morning commute',
    spot: 'People are diligent; even at an early hour, the subway was packed with people, and it was still dark outside',
    date: '2024.12.11',
    type: 'image',
    src: 'src/assets/images/image1.webp',
  },
  {
    title: 'The alley behind the office',
    spot: 'On a cold winter’s early morning commute, there are no people around, and the streetlights glow warmly.',
    date: '2024.12.11',
    type: 'image',
    src: 'src/assets/images/image2.webp',
  },
  {
    title: 'French grocery store',
    spot: 'A newly opened specialty store for French cooking ingredients feels unfamiliar to me. Will I ever get a chance to visit it?',
    date: '2024.12.11',
    type: 'image',
    src: 'src/assets/images/image3.webp',
  },
  {
    title: 'Starbugs',
    spot: 'In the early morning, the warm lights of a distant Starbucks catch my eye. I wish I could go in and enjoy a warm cup of coffee.',
    date: '2024.12.11',
    type: 'image',
    src: 'src/assets/images/image4.webp',
  },
];

const shuffleArray = (array: Contents) => {
  array.forEach((item: Content, index: number) => {
    const randomIndex = Math.floor(Math.random() * (index + 1));
    [array[index], array[randomIndex]] = [array[randomIndex], array[index]];
  });
  return array;
};

const contents = ref(shuffleArray(defaultContents));

onMounted(() => {});
</script>

<style scoped>
.container {
  position: relative;
  width: 100%;
  height: 100vh;
  background-color: #000;
  min-width: 480px;
}
.info {
  position: absolute;
  left: 50%;
  bottom: 8%;
  transform: translateX(-50%);
  width: min(90%, 480px);
  text-align: center;
  z-index: 101;
  padding: 1.5rem 1.25rem;
  border-radius: var(--radius-m);
  border: 1px solid rgba(255, 255, 255, 0.12);
}

.theme_1 {
  color: #000;
  background-color: rgba(255, 255, 255, 0.4);
}

.theme_2 {
  color: var(--color-dark-text);
  background-color: rgba(18, 18, 20, 0.35);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}

.theme_3 {
  color: #fff;
}

.info__title {
  font-family: var(--font-display);
  font-weight: 600;
  font-size: 1.1rem;
}

.info__spot {
  margin: 0.6rem auto 0;
  width: 90%;
  color: var(--color-dark-muted);
  font-size: 14px;
  letter-spacing: -0.2px;
}

.info__date {
  margin-top: 0.4rem;
  color: var(--color-accent);
  font-size: 13px;
  font-variant-numeric: tabular-nums;
}

.bg {
  height: 100%;
}

.bg__image {
  width: 100%;
  height: 100%;
  background-color: #ccc;
  background-size: cover;
  background-position: center center;
  filter: brightness(1.2) contrast(1.1) blur(1px);
  opacity: 1;
}

.bg__vignette {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle, rgba(0, 0, 0, 0) 50%, rgba(0, 0, 0, 0.5) 100%);
  pointer-events: none; /* 클릭 이벤트를 차단하여 하위 요소에 전달 */
  z-index: 100;
}

.copyright {
  position: absolute;
  left: 0;
  top: 94%;
  width: 100%;
  color: var(--color-dark-muted);
  text-align: center;
  font-size: 13px;
  z-index: 101;
}
</style>
