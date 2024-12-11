<template>
  <section class="container">
    <div class="info">
      <h2 class="info__title">" {{ activeContent.title.toUpperCase() }} "</h2>
      <p class="info__spot">{{ activeContent.spot }}</p>
      <p class="info__date">{{ activeContent.date }}</p>
    </div>
    <div class="bg">
      <div class="bg__vignette"></div>
      <div id="bg-image" class="bg__image"></div>
    </div>
    <p class="copyright">reodavin@gmail.com / 010.3258.6912</p>
  </section>
</template>

<script setup lang="ts">
import { type Ref, ref, onMounted } from 'vue';
// const title: Ref<string> = ref('Starbugs'.toUpperCase());
// const spot: Ref<string> = ref(
//   'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Dolor, incidunt.',
// );
// const date: Ref<string> = ref('2024.12.11');

const defaultContents = [
  {
    title: 'Early morning commute',
    spot: 'People are diligent; even at an early hour, the subway was packed with people, and it was still dark outside',
    date: '2024.12.11',
    src: 'src/assets/images/image1.jpeg',
  },
  {
    title: 'The alley behind the office',
    spot: 'On a cold winter’s early morning commute, there are no people around, and the streetlights glow warmly.',
    date: '2024.12.11',
    src: 'src/assets/images/image2.jpeg',
  },
  {
    title: 'French grocery store',
    spot: 'A newly opened specialty store for French cooking ingredients feels unfamiliar to me. Will I ever get a chance to visit it?',
    date: '2024.12.11',
    src: 'src/assets/images/image3.jpeg',
  },
  {
    title: 'Starbugs',
    spot: 'In the early morning, the warm lights of a distant Starbucks catch my eye. I wish I could go in and enjoy a warm cup of coffee.',
    date: '2024.12.11',
    src: 'src/assets/images/image4.jpeg',
  },
];

const contents = ref(defaultContents);
const shuffleNumber: Ref<number> = ref(Math.floor(Math.random() * contents.value.length));
const activeContent = ref(contents.value[shuffleNumber.value]);

const setBackgorundImage = () => {
  const ele = document.getElementById('bg-image');
  if (ele) {
    ele.style.backgroundImage = `url(${activeContent.value.src})`;
  }
};

onMounted(() => {
  setBackgorundImage();
});
</script>

<style scoped>
.container {
  position: relative;
  width: 100%;
  height: 100vh;
}
.info {
  position: absolute;
  left: 0;
  top: 47%;
  width: 100%;
  color: #fff;
  text-align: center;
  z-index: 101;
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
  filter: brightness(1.1) contrast(1.1) blur(1px);
  /* opacity: 0.6; */
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
  opacity: 0.7;
  z-index: 101;
}
</style>
