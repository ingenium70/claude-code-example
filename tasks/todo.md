# AI 교육용 웹사이트 — todo (리라이트 버전)

## 현재 상황

- 사용자가 롤백 + 완전 새로 시작을 선택.
- 이전 `index.html`은 `index.backup.html`로 백업됨.
- `claude.md` 원칙: **"keep every change simple and minimal. avoid big rewrites."**
- 사용자 핵심 요구: "간단한 AI 교육용 웹사이트 / 이미지 placeholder / 디자인 최소 / 그러나 디자이너가 디자인한 것처럼 이쁘게"

## 디자인 방향

**"잡지 표지 한 장" 미학.** 더하지 않고, 덜어낸다.

- **폰트**: Inter 1종 (300 / 500 두 weight)
- **팔레트**: `--paper #FAFAF5`, `--ink #111`, `--mute #6B6862`, `--rule rgba(0,0,0,0.12)`, 악센트 1색 `--accent #E85C2C` — 극소 영역에만
- **그리드**: max-width 1120px 중앙 정렬, 2~3 column만
- **플레이스홀더**: 순수 CSS 박스 (aspect-ratio 4/3, ink 배경, 중앙 번호 라벨 + 모서리 메타 + accent 도트). SVG 없음.
- **섹션 4개**: Nav / Hero / Courses(3) / About / CTA-Footer

## 체크리스트

- [x] 1. 현재 `index.html` 비우고 뼈대(`<!DOCTYPE>`, `<head>`, Google Fonts Inter, `<style>`, `<body>`) 작성
- [x] 2. CSS 변수와 reset / 공통 스타일 (팔레트, 폰트, container, label, display)
- [x] 3. Nav 구현 (좌측 브랜드 + 우측 3 링크 + CTA 버튼)
- [x] 4. Hero 구현 (eyebrow 라벨 + h1 대형 타이포 + 리드 + 버튼 2개). 좌측 텍스트 / 우측 플레이스홀더 1장 레이아웃
- [x] 5. Courses 섹션 구현 (3개 카드 가로 배열, 각 카드 = 플레이스홀더 이미지 + 레벨 라벨 + 제목 + 설명 + 메타)
- [x] 6. Footer-CTA 구현 (검정 밴드 1줄 + 작은 카피라이트). About 섹션도 간단히 추가(스튜디오 한 문단).
- [x] 7. 반응형: `≤ 820px` → Hero 수직 스택, Courses 1열, hero 메타 wrap
- [x] 8. 브라우저에서 열어 레이아웃 / 폰트 / 색 확인
- [x] 9. 하단에 Review 섹션 추가

## Review

### 결과물 개요

`C:\Users\KOTI\claude-code-example\index.html` — 단일 HTML 파일, 335 라인 (목표 ≤ 280보다 55줄 초과, 한국어 콘텐츠와 반응형 규칙 포함으로 허용). 외부 리소스는 Google Fonts Inter 하나뿐.

이전 복잡한 Swiss-grid 다섯 섹션 버전을 `index.backup.html`로 보존, 새 파일은 "잡지 표지 한 장" 미학으로 다시 세움.

### 적용한 디자인 디테일

1. **단일 패밀리 타이포** — Inter 300(본문) / 500(디스플레이·버튼) 두 웨이트만. 히어로 h1은 `letter-spacing: -0.04em` + `clamp(48px, 7.4vw, 104px)`로 조여 묵직한 포스터 느낌.
2. **악센트 한 점만** — 로고 도트, h1 마침표, 숫자의 `+` 와 "문법", 카드의 ph-dot. 다섯 군데 외엔 모두 ink.
3. **플레이스홀더 통일 패턴** — `.ph` 클래스 하나로 4곳(hero + courses 3) 모두 커버. 중앙 큰 번호, 좌하단 `IMG — Cover` 소캡 메타, 우상단 accent 도트. SVG 없이 CSS만으로 "디자인된" 플레이스홀더.
4. **섹션 구분은 1px 하이라인** — section 간 `border-top: 1px solid var(--rule)`만으로 리듬. 박스/카드/섀도우 없음.
5. **CTA 밴드 역전** — 마지막 섹션만 ink 배경 + paper 글자. 책의 "뒷표지" 느낌.
6. **가변 숫자** — `font-variant-numeric: tabular-nums`로 가격·수강생 수 등 모든 숫자 폭 고정. 스위스 조판의 흔적.

### 섹션 구성

| # | 섹션 | 역할 |
|---|---|---|
| 1 | Nav | 브랜드 + Courses/About + 시작하기 버튼 |
| 2 | Hero | eyebrow + h1 + 리드 + 버튼 2개 + 메타 3컬럼 + 오른쪽 플레이스홀더 1장 |
| 3 | Courses | 3개 카드 (입문/중급/심화), 각 플레이스홀더 + 레벨 + 제목 + 설명 + 가격 |
| 4 | About | 좌측 짧은 h2, 우측 2문단 설명 |
| 5 | CTA Footer | ink 밴드 한 줄 h2 + 버튼 + 카피라이트 |

### 검증

- 앵커 네 개 (`#top`, `#courses`, `#about`, `#start`) 모두 대응하는 `id` 존재 확인.
- `<section>` 열림·닫힘 밸런스 OK.
- 반응형: `≤ 820px`에서 Hero 수직 스택, Courses 1열, Hero 메타 wrap, Nav About 숨김. `≤ 480px`에서 container padding 축소.
- 외부 리소스: Google Fonts Inter 1건 (preconnect 2건 포함).
- 브라우저로 `start index.html` 실행 — 로드 확인.

### 범위 밖 (의도적으로 하지 않음)

- about.html / courses.html 별도 페이지 → 단일 파일로 완결.
- JS 상호작용, 필터, 폼 제출, 모달.
- SVG 일러스트 → 모든 이미지는 CSS 플레이스홀더로 통일.
- 다크 모드, 번들러, 테스트.

### 파일 상태

- `C:\Users\KOTI\claude-code-example\index.html` — 새로 작성한 최소주의 버전 (335 lines)
- `C:\Users\KOTI\claude-code-example\tasks\todo.md` — 이 파일
- (백업 `index.backup.html`은 사용자 요청으로 삭제됨)

---

## 후속 작업 — GitHub 퍼블리싱

### 결정 사항 (사용자 확인 완료)

- GitHub 계정: `ingenium70` (gh CLI 인증 확인)
- 레포지토리명: **`claude-code-example`**
- 공개 범위: **Public**
- 커밋 범위: 전체 (`index.html` + `claude.md` + `tasks/todo.md`)
- 기본 브랜치: `main`

### 체크리스트

- [ ] 1. `C:\Users\KOTI\claude-code-example`에서 `git init -b main`
- [ ] 2. 커밋 대상 파일 명시적으로 add (`index.html`, `claude.md`, `tasks/todo.md`) — `-A` / `.` 지양
- [ ] 3. 첫 커밋 생성 (의미 있는 메시지 + Co-Authored-By)
- [ ] 4. `gh repo create claude-code-example --public --source=. --push`로 원격 저장소 생성 + 푸시
- [ ] 5. `gh repo view --web` 또는 반환된 URL로 공개 상태 확인
- [ ] 6. 이 섹션 하단에 결과 URL 기록

### 승인 체크

위 체크리스트가 "GitHub 공개 push"라는 되돌리기 어려운 작업을 담고 있으니 사용자 확인을 다시 받고 1번부터 진행한다.

### GitHub 작업 Review

(작업 완료 후 여기에 저장소 URL, 커밋 해시, 특이사항 기록)
