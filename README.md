# May World

사진 갤러리와 골프장 리스트를 담은 개인용 Vue 3 SPA. 백엔드 없이 정적 자산과
더미 데이터로 동작한다. 디자인 방향은 "에디토리얼 모노크롬"
([`DESIGN.html`](./DESIGN.html), [`docs/DESIGN.md`](./docs/DESIGN.md) 참고).

## 화면 구성

- `/` — 홈: 히어로 + 기능 소개
- `/gallery` — 풀스크린 스와이프 포토 갤러리
- `/golf-courses` — 골프장 리스트 (코스/그린 난이도 필터)
- `/about` — 프로젝트 소개

## 기술 스택

Vue 3 (Composition API, `<script setup>`) · TypeScript · Vite 6 · vue-router 4 ·
Pinia · vue-awesome-swiper

## 문서

에이전트/신규 기여자는 작업 전에 아래 문서를 먼저 읽는다.

- [`docs/ARCHITECTURE.md`](./docs/ARCHITECTURE.md) — 디렉터리 구조, 라우트,
  데이터 흐름, 알려진 제약(스캐폴드 잔재 등)
- [`docs/CONVENTION.md`](./docs/CONVENTION.md) — 컴포넌트/TS/스타일/데이터
  작성 규칙
- [`docs/SECURE.md`](./docs/SECURE.md) — 이 정적 SPA의 위협 모델과 보안 원칙
- [`docs/DESIGN.md`](./docs/DESIGN.md) — 컬러/타이포/컴포넌트 토큰
  (`DESIGN.html` 스타일 타일과 동기화)

## 프로젝트 설정

```sh
npm install
```

### 개발 서버

```sh
npm run dev
```

### 타입 체크 + 프로덕션 빌드

```sh
npm run build
```

### 린트 / 포맷

```sh
npm run lint
npm run format
```

## 권장 IDE 설정

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
(Vetur는 비활성화). `.vue` 파일의 타입 체크는 `vue-tsc`(`npm run type-check`)로
수행한다.
