# ARCHITECTURE

May World는 사진 갤러리와 골프장 리스트를 담은 개인용 Vue 3 SPA다. 백엔드 없이
클라이언트 정적 자산 + 인메모리 더미 데이터로 동작한다. 이 문서는 에이전트가
매번 코드를 재탐색하지 않고도 구조를 파악할 수 있도록 하는 것이 목적이다.

## 기술 스택

| 영역 | 선택 | 비고 |
| --- | --- | --- |
| 프레임워크 | Vue 3 (`<script setup>`, Composition API) | 클래스 컴포넌트/Options API 미사용 |
| 언어 | TypeScript | `vue-tsc`로 타입 체크 (`npm run type-check`) |
| 빌드 | Vite 6 | `vite-plugin-vue-devtools` 활성화 |
| 라우팅 | vue-router 4 | `src/router/index.ts`, lazy-loaded 라우트 |
| 상태 관리 | Pinia | 현재 `stores/counter.ts`는 템플릿이 남긴 미사용 예시 (실제 화면은 로컬 `ref`/`computed`만 사용) |
| 슬라이더 | vue-awesome-swiper | GalleryView 풀스크린 슬라이드에만 사용 |
| 배포 대상 | 정적 호스팅 | 인증/서버 API 없음 |

## 디렉터리 구조

```
src/
  App.vue              # 전역 nav + 라우터 아웃렛, fullBleed 레이아웃 분기
  main.ts              # 앱 부트스트랩 (Pinia, Router 등록)
  router/index.ts       # 라우트 정의 (/,/gallery,/golf-courses,/about)
  views/                # 라우트 단위 페이지 컴포넌트 (실질적인 화면 단위)
  components/           # create-vue 스캐폴드 잔재 — 실사용 안 됨 (아래 참고)
  data/golfCourses.ts    # 골프장 더미 데이터 + 헬퍼(getRandomEmoji)
  stores/counter.ts      # Pinia 사용 예시, 실제 화면에서 참조 안 됨
  assets/
    base.css, main.css   # 디자인 토큰(CSS 변수) + 전역 리셋
    images/               # 갤러리용 webp 원본
docs/                   # 이 문서들
DESIGN.html             # 디자인 방향 리뷰용 스타일 타일 (docs/DESIGN.md와 세트)
```

### 라우트 ↔ 화면 매핑

- `/` → `HomeView.vue`: 히어로 + 기능 소개, 다른 라우트로의 진입점.
- `/gallery` → `GalleryView.vue`: `meta.fullBleed: true`. 전체화면 스와이프 갤러리,
  `App.vue`가 이 플래그를 보고 nav를 오버레이로, main 패딩을 0으로 바꾼다.
- `/golf-courses` → `GolfCourseListView.vue`: `data/golfCourses.ts`의 더미 배열을
  로컬 상태로 필터링/정렬하는 리스트 화면.
- `/about` → `AboutView.vue`: 정적 소개/연락처 텍스트.

### 스캐폴드 잔재 (주의)

`components/HelloWorld.vue`, `TheWelcome.vue`, `WelcomeItem.vue`, `components/icons/*`,
`stores/counter.ts`는 `create-vue` 템플릿이 생성한 기본 예시로, 어떤 실제 화면에서도
import되지 않는다. 새 기능을 이 파일들 위에 얹지 말 것 — 필요하면 신규 컴포넌트를
만들고, 이 잔재는 별도 정리 태스크(사용자 승인 후)로 제거한다.

## 데이터 흐름

- **정적 더미 데이터만 존재.** `golfCourses.ts`의 배열이 유일한 "DB" 역할이며,
  API 호출/원격 fetch는 없다. 새 데이터 소스를 붙일 계획이라면 이 파일을 대체할
  fetch 계층을 어디에 둘지(예: `src/api/`) 먼저 설계하고 진행한다.
- `GalleryView.vue`의 슬라이드 콘텐츠(`defaultContents`)도 컴포넌트 내부에
  하드코딩되어 있다 — `assets/images/imageN.webp`를 가리키는 로컬 배열.
- 필터링/정렬 로직은 각 뷰의 `computed` 안에 있다 (전역 스토어 없음). 여러 화면이
  같은 필터 상태를 공유해야 하는 요구가 생기면 그때 Pinia 스토어 도입을 검토한다
  (미리 만들어두지 않는다 — YAGNI).

## 레이아웃 규칙

`App.vue`가 라우트 `meta.fullBleed`를 읽어 두 가지 레이아웃 모드를 만든다:

1. 기본: sticky nav + `max-width: 1200px` 중앙 정렬 컨텐츠.
2. `fullBleed: true`: nav가 `position: fixed` + 글래스모피즘 오버레이로 바뀌고,
   메인 영역 패딩/max-width가 제거된다 (전체화면 이미지 슬라이드용).

새 라우트를 추가할 때 이 두 모드 중 어디에 속하는지 먼저 정하고 `meta.fullBleed`를
명시한다.

## 디자인 토큰 연결

`src/assets/base.css`가 `--color-*`, `--font-*`, `--radius-*`, `--motion-*` CSS
변수를 정의하는 단일 소스다. 이 값들은 [[../DESIGN.html]] / `docs/DESIGN.md`의
"에디토리얼 모노크롬" 방향과 1:1로 맞춰져 있어야 한다. 컴포넌트 스타일에서 hex
값을 직접 쓰지 않고 반드시 이 변수를 통해 참조한다.

## 알려진 제약

- 테스트 스위트, CI 워크플로(`.github/`) 없음 — 변경 후 최소 `npm run type-check`,
  `npm run lint`, `npm run build`로 수동 검증한다.
- 서버/인증/DB 없음 — 보안 고려사항은 정적 호스팅 관점으로 한정된다
  (`docs/SECURE.md` 참고).
