# Project Roadmap — vanguarddream.github.io

이 파일은 포트폴리오 사이트의 **목적, 개발 방향, 콘텐츠 기준, 워크플로우**를 정의합니다.  
컨텍스트가 초기화된 새 대화에서도 이 파일을 읽으면 프로젝트의 일관성을 유지할 수 있습니다.

---

## 1. 사이트 개요

| 항목 | 내용 |
|------|------|
| **소유자** | Bongsub Song (송봉섭) |
| **소속** | ETRI (전자통신연구원) — Intelligent Robot System Research Section |
| **URL** | https://vanguarddream.github.io |
| **기술 스택** | Jekyll, jekyll-theme-minimal, GitHub Pages |
| **목적** | 연구 성과(논문, 프로젝트)를 정리하는 개인 포트폴리오 |

---

## 2. 사이트 구조 (네비게이션)

```
/           → index.md        (Home)     — 프로필, 경력, 교육, 논문 목록, 미디어
/projects   → projects.md     (Projects) — 연구과제 목록 및 상세
/publications → publications.md (Publications) — 논문 목록 + 상세 페이지 링크
/papers/<id>  → papers/<id>.md  (개별 논문 상세 페이지)
```

**사이드바 링크:** `_config.yml`의 `sidebar_links`에서 관리.

---

## 3. 콘텐츠 기준

### 3-1. Home (`index.md`)
- 최상단: 이름, 소속, 연락처, 뱃지 링크 (LinkedIn, Google Scholar, ETRI)
- Biography, Professional Experiences, Education, Skills
- Research Projects (간략 목록)
- Publications (전체 목록 — 저널/학회 구분)
- Honors & Awards, Patents, Media Appearances

### 3-2. Projects (`projects.md`)
- 연구 과제 단위로 기술
- 각 항목: `기관/과제`, `기간`, `키워드`, `한 줄 요약`, `내가 한 일`
- 목차(앵커 링크) + 세부 섹션 구조 유지

### 3-3. Publications (`publications.md`)
- 저널 논문: 번호 목록, 상세 페이지가 있으면 `→ [View Details](/papers/<id>)` 링크
- 학회 논문: 불릿 목록, 동일 방식
- 상세 페이지가 없는 논문은 링크 생략 (나중에 추가 가능)

### 3-4. 논문 상세 페이지 (`papers/<id>.md`)
다음 섹션 순서를 기본 템플릿으로 사용:
1. ← Back to Publications 링크
2. 논문 제목 (h1)
3. Journal/Conference, Authors, Keywords
4. Abstract
5. Key Contributions (불릿)
6. 섹션별 그림 + 캡션 (논문 구성에 맞게 조정)
7. ← Back to Publications 링크 (하단)

---

## 4. 새 논문 추가 워크플로우

새 논문 결과물을 사이트에 추가할 때 따르는 표준 절차.

### Step 1 — 소스 자료 준비
```
source/<VENUE><YEAR>/       ← 이 폴더는 gitignore됨 (배포 불가)
  ├── main.tex
  └── fig/  또는  figure/
        ├── fig1.jpg
        └── ...
```

### Step 2 — 핵심 그림 선별 및 복사
- 논문에서 **페이지에 보여줄 핵심 그림** 5–10장 선별
- `assets/papers/<id>/` 폴더에 복사 (이 경로만 GitHub Pages에 배포됨)

```bash
mkdir -p assets/papers/<id>
cp source/<VENUE><YEAR>/fig/fig1.jpg assets/papers/<id>/
# ... 필요한 그림 반복
```

### Step 3 — 논문 상세 페이지 작성
- `papers/<id>.md` 생성
- Front matter:
  ```yaml
  ---
  layout: default
  title: "논문 제목"
  description: "SEO용 1–2줄 설명"
  ---
  ```
- 섹션 구성: Abstract → Key Contributions → 그림 포함 본문 → Back 링크
- 이미지 경로: `/assets/papers/<id>/파일명.jpg`

### Step 4 — publications.md 업데이트
- 해당 논문 항목에 `→ [View Details](/papers/<id>)` 링크 추가

### Step 5 — index.md 업데이트 (필요 시)
- Publications 섹션의 논문 목록에 새 항목 추가

### Step 6 — 변경 로그 기록
- `CLAUDE_CHANGES.md`에 세션 항목 추가

---

## 5. 개발 이정표

### ✅ 완료
- [2026-03-31] 사이트 기본 구조 완성 (Home, Projects 탭)
- [2026-03-31] Publications 탭 구축 — 전체 논문 목록 + 3편 상세 페이지
  - ICAE 2025: 뱀 로봇 보행 최적화 (GD/GPG)
  - IROS 2024: GripFlexer 하이브리드 그리퍼
  - Sensors & Actuators A 2024: 전기흡착 필름 하이브리드 그리퍼
- [2026-03-31] 프로젝트 문서화 체계 수립 (CLAUDE_CHANGES.md, PROJECT_ROADMAP.md)

### 🔲 단기 목표 (Priority: High)
- [ ] 나머지 저널 논문 상세 페이지 추가
  - Nuclear Engineering and Technology 2023 (PBIS 논문)
  - Nuclear Engineering and Technology 2020 (Depth-adaptive controller)
- [ ] index.md Publications 섹션에서 상세 페이지 링크 연결 (현재 publications.md에만 링크 있음)
- [ ] 모바일 뷰 레이아웃 확인 및 필요 시 조정

### 🔲 중기 목표
- [ ] 새 논문 게재 시 즉시 상세 페이지 추가 (워크플로우 Step 1–6 적용)
- [ ] Projects 페이지 — 각 과제별 대표 이미지/결과물 추가
- [ ] Google Scholar 인용 수 또는 DOI 링크 추가

### 🔲 장기 목표
- [ ] 강화학습 기반 뱀 로봇 연구 (Ph.D. thesis 핵심) 별도 상세 페이지
- [ ] ETRI 재직 중 신규 연구 결과물 지속 추가

---

## 6. 설계 원칙 및 규칙

| 원칙 | 내용 |
|------|------|
| **source/ 접근 금지** | `source/`는 gitignore됨. 이미지는 반드시 `assets/papers/<id>/`로 복사 후 사용 |
| **이미지 원본 파일명 유지** | 복사 시 파일명 변경 없이 유지 (추적 용이) |
| **언어** | 사이트 콘텐츠는 영어, 개인 메모/설명은 한국어 혼용 허용 |
| **레이아웃** | 모든 페이지 `layout: default` 사용 |
| **날짜 형식** | YYYY-MM-DD (국제 표준) |
| **변경 기록** | 모든 Claude 세션의 변경 사항은 `CLAUDE_CHANGES.md`에 기록 |

---

## 7. 파일 구조 참조

```
vanguarddream.github.io/
├── _config.yml              # 사이트 설정, sidebar_links
├── _layouts/
│   └── default.html         # 공통 레이아웃
├── assets/
│   ├── profile.jpg
│   ├── etri.jpg, kaeri.jpg, kiost.jpg, cnn_broadcast.jpg
│   └── papers/
│       ├── icae2024/        # ICAE 2025 논문 figure
│       ├── iros2024/        # IROS 2024 논문 figure
│       └── saap2024/        # Sensors & Actuators A 2024 논문 figure
├── papers/
│   ├── icae2024.md          # 논문 상세 페이지
│   ├── iros2024.md
│   └── saap2024.md
├── source/                  # ← GITIGNORED (LaTeX 원본, 배포 불가)
│   ├── ICAE2024-rev/
│   ├── IROS2024/
│   └── SAAP2024/
├── index.md                 # Home 탭
├── projects.md              # Projects 탭
├── publications.md          # Publications 탭
├── CLAUDE_CHANGES.md        # Claude 변경 로그
└── PROJECT_ROADMAP.md       # 이 파일 (프로젝트 방향/이정표)
```

---

*이 파일은 새 연구 결과가 추가되거나 개발 방향이 변경될 때마다 업데이트합니다.*  
*최종 수정: 2026-03-31*
