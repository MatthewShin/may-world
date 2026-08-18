# DESIGN

디자인 방향은 **"에디토리얼 모노크롬"** — 무드 있는 사진 갤러리와 골프장
리스트를 하나의 절제된 편집 언어로 묶는다. 넓은 흑백·웜그레이 톤 위에
타이포그래피와 여백으로 위계를 만들고, 앰버 골드 하나만 강조색으로 쓴다.

지향: 절제된 / 사진 중심 / 명료함
지양: 유아틱함, 과잉 장식

> 인터랙티브 리뷰용 스타일 타일은 저장소 루트의 [`DESIGN.html`](../DESIGN.html)에
> 있다. 이 문서는 그 내용을 코드에서 바로 참조 가능한 형태로 요약·고정한 것이다.
> **`DESIGN.html`을 갱신하면 이 문서도, 이 문서를 바꾸면 실제 구현
> (`src/assets/base.css`)도 같이 맞춘다** — 세 곳이 항상 동기화되어 있어야 한다.

## 컬러 토큰

`src/assets/base.css`의 `--color-*` 변수와 1:1 대응. 컴포넌트에서는 반드시
변수로 참조하고 hex를 직접 쓰지 않는다 ([[CONVENTION.md]] 참고).

| 역할 | 변수 | 라이트 | 다크 | 용도 |
| --- | --- | --- | --- | --- |
| ink | `--color-ink` | `#15171B` | `#F2F0EA` | 제목/본문/기본 버튼 배경 |
| paper | `--color-paper` | `#F6F4EF` | `#121214` | 기본 배경(canvas) |
| surface | `--color-surface` | `#FFFFFF` | `#1B1C1F` | 카드/인풋/팝오버 |
| surface-sunken | `--color-surface-sunken` | `#EFECE4` | `#202125` | 인셋 영역 |
| muted | `--color-muted` | `#6B6D72` | `#A4A3A0` | 보조 텍스트/라벨 |
| border | `--color-border` | `#E4E1D8` | `#313236` | 카드·인풋 경계 (장식용) |
| border-strong | `--color-border-strong` | `#CFCCC1` | `#45464B` | 강조 경계, hover |
| accent | `--color-accent` | `#A97524` | `#D5A153` | 활성 필터, 별점 채움, 핵심 hover |
| accent-ink | `--color-accent-ink` | `#7A5619` | `#E8C07F` | 링크, accent 텍스트 |
| success | `--color-success` | `#2F7A4C` | — | 저장/적용 완료 상태 |
| warning | `--color-warning` | `#A4560F` | — | 경고 |
| error | `--color-error` | `#B5372A` | — | 입력 오류, 리셋 활성 강조 |
| dark canvas | `--color-dark-canvas` | `#121214` | — | 사진 히어로, 다크 표면(라이트 모드에서도 고정) |

**규칙:** accent(`#A97524`)는 흰 배경 위 작은 텍스트에 쓰지 않는다 — 큰
텍스트/아이콘/경계선에만. 다크 캔버스 위 accent 대비는 5.8:1로 통과.

## 타이포그래피

- **Display**: Fraunces 500/600 (`--font-display`) — 페이지 타이틀, 섹션
  타이틀, 갤러리 캡션. 에디토리얼한 무게감이 목적.
- **Body/UI**: Inter 400–700 (`--font-body`) — 본문, 라벨, 필터, 데이터.
- 라벨은 Inter 600, 소문자 대신 대문자 + `letter-spacing: 0.04–0.06em`.
- 숫자 데이터(전장, 난이도 등)는 `font-variant-numeric: tabular-nums`로 정렬.

| 용도 | 폰트/굵기 | 크기 |
| --- | --- | --- |
| H1 / 히어로 | Fraunces 600 | `clamp(2.25rem, 4vw, 3.4rem)` / line-height 1.08 |
| H2 / 섹션 타이틀 | Fraunces 600 | ~1.6–2rem |
| Body | Inter 400 | 1rem / line-height 1.6 |
| Label | Inter 600 | 0.8rem, uppercase |
| Data | Inter, tabular-nums | 0.9–0.95rem |

폰트는 Google Fonts에서 로드 (`index.html`의 `<link>`) — `Fraunces:opsz,wght@9..144,500;9..144,600`,
`Inter:wght@400;500;600;700`.

## Foundations

- **간격**: 4 / 8 / 16 / 24 / 40 / 64px 스케일.
- **반경**: `--radius-s: 4px`(인풋/버튼), `--radius-m: 8px`(카드/패널),
  `--radius-pill: 999px`(칩/배지).
- **경계/그림자**: 1px 실선 경계 우선, 그림자는 최소한
  (`--shadow-1: 0 1px 2px rgba(21,23,27,.06)`). 깊이는 그림자보다 크기·위치·
  색면으로 표현한다.
- **모션**: `--motion-fast: 160ms ease-out`, `--motion-base: 200ms ease-out`.
  위치·투명도 변화만 사용, 바운스 등 과장된 이징 금지.
  `prefers-reduced-motion: reduce`에서 전환 생략 (`base.css`에 이미 적용됨).

## 컴포넌트 패턴

- **버튼**: `btn-primary`(ink 배경, hover 시 accent-ink), `btn-secondary`
  (투명 배경 + border-strong), `btn-ghost`(텍스트만). 모든 버튼에
  `focus-visible` 아웃라인(accent, 2px) 필수.
- **필터 (select/chip)**: 라벨은 muted + uppercase, 에러 상태는 error 색
  border + 에러 메시지. 활성 칩은 accent border + accent-ink 텍스트 +
  `rgba(169,117,36,0.1)` 배경.
- **별점/난이도**: 채워진 도트는 accent, 빈 도트는 border-strong. 실제 구현
  (`GolfCourseListView.vue`)은 🐶(코스 난이도)/🐰(그린 난이도) 이모지로
  변형되어 있다 — 스타일 타일의 `●/○` 패턴과 동일한 "채움 vs 흐림" 원칙만
  지키면 이모지 표현은 허용.
- **글래스모피즘은 갤러리 nav 오버레이 한 곳에만** 보조로 적용
  (`backdrop-filter: blur(12px)` + `rgba(18,18,20,0.35)`). 다른 화면에
  확산 금지 — 이 방향은 "절제"가 핵심이므로 장식 효과를 최소한으로 유지한다.

## 대표 화면 방향

- **갤러리**: 다크 풀블리드 사진 히어로 + 하단 캡션 카드(글래스모피즘) +
  스와이프. (`GalleryView.vue`, `meta.fullBleed`)
- **골프장 리스트**: 라이트 표면 위 카드 리스트, accent로 필터 활성/난이도
  강조. (`GolfCourseListView.vue`)

## 변경 절차

1. 팔레트/타이포/컴포넌트를 바꾸고 싶으면 먼저 `DESIGN.html`을 수정해
   시각적으로 리뷰한다.
2. 승인되면 이 문서(`docs/DESIGN.md`)의 표/설명을 갱신한다.
3. 마지막으로 `src/assets/base.css`(및 필요 시 컴포넌트 스타일)를 갱신해
   실제 화면에 반영한다.

이 순서를 지키지 않고 `base.css`만 바꾸면 스타일 타일/문서가 실제 구현과
어긋나 다음 작업 때 잘못된 기준으로 판단하게 된다.
