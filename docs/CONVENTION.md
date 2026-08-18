# CONVENTION

이 프로젝트에서 코드를 작성/수정할 때 지키는 구체적 규칙. 전역 규칙(커밋 메시지
형식, 확인 절차 등)은 `~/.claude/CLAUDE.md`를 따르며, 여기서는 이 저장소에만
해당하는 세부 컨벤션만 다룬다.

## 컴포넌트 (Vue SFC)

- `<script setup lang="ts">` + Composition API만 사용한다. Options API,
  클래스 컴포넌트 금지.
- SFC 블록 순서: `<template>` → `<script setup>` → `<style scoped>`.
  `scoped` 없이 전역 스타일을 여는 경우는 `assets/main.css`, `assets/base.css`
  뿐이다.
- 라우트에 매핑되는 페이지 단위 컴포넌트는 `src/views/*View.vue`, 재사용
  컴포넌트는 `src/components/*.vue`에 둔다. 파일명은 PascalCase.
- 새 컴포넌트를 `components/`에 추가하기 전에 기존 스캐폴드 잔재
  (`HelloWorld.vue` 등, [[ARCHITECTURE.md]] 참고)를 재사용하려 하지 말 것 —
  전부 미사용 예시 코드다.

## TypeScript

- `interface`로 도메인 타입 정의 (`GolfCourse` 참고), 데이터/타입은
  `src/data/*.ts`에 함께 둔다.
- `any` 금지. props/emit은 반드시 타입을 명시한다.
- 절대 경로 alias `@/*` → `src/*` 사용 가능 (`tsconfig.app.json`), 다만 기존
  코드는 상대경로(`../data/...`)를 많이 쓴다 — 같은 디렉터리 내에서는 기존
  스타일을 따르고, 깊은 경로에서는 `@/` alias를 우선한다.

## 스타일 / 디자인 토큰

- 색상·폰트·반경·모션 값은 항상 `src/assets/base.css`의 CSS 변수
  (`--color-*`, `--font-*`, `--radius-*`, `--motion-*`)로 참조한다. hex 코드나
  매직 넘버를 컴포넌트 스타일에 직접 쓰지 않는다.
- 새 색상/타이포 토큰이 필요하면 `docs/DESIGN.md`에 먼저 정의하고 승인받은
  뒤 `base.css`에 추가한다 — 컴포넌트 스타일에서 즉흥적으로 만들지 않는다.
- 반응형 브레이크포인트는 기존 코드가 쓰는 `@media (max-width: 768px)` /
  `770px`에 맞춘다 (통일된 breakpoint 변수는 아직 없음 — 새로 도입하려면
  전역 영향이 있으니 먼저 계획을 세운다).

## 데이터

- 더미 데이터를 추가/수정할 때는 `src/data/golfCourses.ts`의 기존 톤(과장된
  드립성 골프장 이름 등)을 유지한다. 실제 개인정보나 실존 업체명을 넣지 않는다.
- 정렬/필터 로직은 뷰 컴포넌트의 `computed` 안에 두는 현재 패턴을 유지한다.
  여러 화면이 상태를 공유해야 할 때만 Pinia 스토어를 새로 설계한다.

## 언어 / 텍스트

- UI 텍스트, 커밋 메시지, 문서(`README.md`, `docs/*.md`)는 한글로 작성한다.
- 코드 식별자(변수/함수/타입명)는 영어 camelCase/PascalCase를 유지한다
  (기존 코드 전체가 이 패턴).

## 린트 / 포맷

- `npm run lint` (`eslint --fix`), `npm run format` (`prettier --write src/`)를
  커밋 전에 돌린다.
- Prettier 설정:세미콜론 유지, 싱글쿼트, `printWidth: 100`
  (`.prettierrc.json`). 별도 설정 없이 기본값을 신뢰한다.
- `npm run type-check` (`vue-tsc --build`)가 통과해야 한다 — `.vue` 파일의
  타입 오류는 일반 `tsc`로는 잡히지 않으니 반드시 이 스크립트를 쓴다.

## 하지 않는 것

- `npm run dev` / `npm run preview` 자동 실행 금지 (전역 규칙, `localhost`는
  사용자가 직접 관리).
- 스캐폴드 잔재 파일 위에 기능 추가 금지 — 필요하면 새 파일을 만든다.
- 범위를 벗어난 리팩토링(예: 전역 상태 관리 도입, 브레이크포인트 시스템 교체)은
  별도 태스크로 분리하고 먼저 계획을 공유한다.
