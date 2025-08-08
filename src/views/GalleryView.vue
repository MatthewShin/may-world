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
  left: 0;
  top: 50%;
  width: 100%;
  text-align: center;
  z-index: 101;
  height: 130px;
  padding: 10px 0;
  margin-top: -65px;
}

.theme_1 {
  color: #000;
  background-color: rgba(255, 255, 255, 0.4);
}

.theme_2 {
  color: #fff;
  background-color: rgba(0, 0, 0, 0.4);
}

.theme_3 {
  color: #fff;
}

.info__title {
  opacity: 0.9;
  font-size: 18px;
  font-weight: 800;
  /* text-decoration: underline; */
}

.info__spot {
  margin: 10px auto 0;
  width: 80%;
  opacity: 0.8;
  font-size: 14px;
  letter-spacing: -0.4px;
}

.info__date {
  opacity: 0.8;
  font-size: 14px;
  text-decoration: underline;
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
  color: #fff;
  text-align: center;
  font-size: 14px;
  opacity: 0.6;
  z-index: 101;
}
</style>
