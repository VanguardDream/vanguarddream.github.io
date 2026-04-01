# Claude Changes Log

이 파일은 Claude와의 협업으로 발생한 모든 코드 변경 사항을 기록합니다.
각 세션마다 **사용자 요청**과 **변경 내용**을 함께 기록하여, 나중에 코드를 읽는 사람이 변경 맥락을 파악할 수 있도록 합니다.

---

## [2026-04-02] Session 2 — Projects 페이지 카드 그리드 리뉴얼 + 프로젝트 상세 페이지 신규 구축

### 사용자 요청

> `source/` 폴더 하위의 프로젝트 결과물(PDF, PPT, MP4)을 바탕으로 `projects.md` 페이지를  
> `publications.md`처럼 그림이 보이는 페이지로 업데이트해달라.  
> 이미지가 아직 없으므로 추후 삽입이 쉽도록 주석으로 이미지 자리를 표시해달라.  
> 모든 페이지는 한국어가 아닌 영문으로 작성.

### 변경 사항

| 파일 | 동작 | 설명 |
|------|------|------|
| `projects.md` | 수정 | 기존 텍스트 목록 → 카드 그리드 레이아웃으로 전면 재작성. 9개 프로젝트 전체 포함, source가 있는 5개에만 상세 페이지 링크 |
| `projects/electro-adhesive-gripper.md` | 신규 | 전기흡착 그리퍼 상세 페이지 (MOTIE, 2018–2019). 이미지 7개 자리 주석 포함 |
| `projects/narrow-space-navigation.md` | 신규 | 협소공간 구조로봇 상세 페이지 (MOTIE, 2019–2021). 이미지 8개 자리 주석 포함 |
| `projects/otg-mobility.md` | 신규 | OTG 모바일플랫폼 상세 페이지 (MOTIE, 2020–2022). 이미지 7개 자리 주석 포함 |
| `projects/drivetrain-study.md` | 신규 | 이동의자유 드라이브트레인 상세 페이지 (Hyundai, 2022–2023). 이미지 5개 자리 주석 + MP4 embed 주석 포함 |
| `projects/ugv-sampling.md` | 신규 | 지상시료채취 UGV 매니퓰레이터 상세 페이지 (KAERI, 2022–2023). 이미지 7개 자리 주석 포함 |

### 주요 결정 사항

- source 폴더 내 PDF는 암호 보호로 내용 추출 불가 → 기존 `projects.md` 텍스트 및 `index.md` 내용 기반으로 섹션 구성
- 이미지 주석 형식: `<!-- TODO: ... -->` 블록 안에 권장 경로, 출처, 실제 img/div HTML을 모두 포함 → 주석 해제만으로 즉시 이미지 표시 가능
- source가 없는 4개 프로젝트(ETRI 2025, MSIT 2025, MOTIE 2022–2025, MOTIE 2022–2024)는 카드만 표시, 링크 없음
- `drivetrain-study.md`에는 `애니메이션_최종본.mp4` embed 주석 별도 포함
- 이미지 권장 경로 패턴: `assets/projects/<project-slug>/`

---

## [2026-03-31] Session 1 — Publications 탭 구축 및 프로젝트 문서화

### 사용자 요청

> `_config.yml`에서 3개의 서브 페이지(Home, Projects, Publish)를 구성하고 싶다.  
> `source/` 폴더 하위에 있는 논문 `.tex` 파일과 관련 figure/table 자료를 바탕으로  
> Publications 탭 콘텐츠를 `.md` 파일로 작성하고 링크해달라.

> 향후 프로젝트를 지속적으로 이어가기 위한 변경점 로그 파일(`CLAUDE_CHANGES.md`)과  
> 개발 방향의 일관성을 유지할 수 있는 중심 파일(`PROJECT_ROADMAP.md`)을 추가해달라.

### 변경 사항

| 파일 | 동작 | 설명 |
|------|------|------|
| `_config.yml` | 수정 | `sidebar_links`에 Publications 탭 항목 추가 (`/publications`) |
| `publications.md` | 신규 | 전체 저널/학회 논문 목록 페이지. 주요 3편은 상세 페이지 링크 포함 |
| `papers/icae2024.md` | 신규 | *Integrated Computer-Aided Engineering* 2025 논문 상세 페이지 (GD/GPG 메서드, 뱀 로봇 보행) |
| `papers/iros2024.md` | 신규 | *IROS 2024* 논문 상세 페이지 (GripFlexer 하이브리드 그리퍼) |
| `papers/saap2024.md` | 신규 | *Sensors and Actuators A* 2024 논문 상세 페이지 (전기흡착 필름 하이브리드 그리퍼) |
| `assets/papers/icae2024/` | 신규 | ICAE2024 논문 figure 14개 (`source/`에서 복사) |
| `assets/papers/iros2024/` | 신규 | IROS2024 논문 figure 9개 (`source/`에서 복사) |
| `assets/papers/saap2024/` | 신규 | SAAP2024 논문 figure 12개 (`source/`에서 복사) |
| `CLAUDE_CHANGES.md` | 신규 | 이 파일 (변경 로그) |
| `PROJECT_ROADMAP.md` | 신규 | 프로젝트 방향 및 이정표 중심 파일 |

### 주요 결정 사항

- `source/` 폴더는 `.gitignore`에 `/source/*`로 등록되어 배포 불가 → 논문 figure는 모두 `assets/papers/<id>/`로 복사 후 링크
- 논문 상세 페이지 경로: `/papers/<id>` (Jekyll이 `papers/` 폴더의 `.md`를 자동 처리)
- 이미지 파일명은 원본 유지 (IROS2024는 한글 파일명 그림N.jpg 형태)

---

<!-- 새 세션을 추가할 때는 아래 템플릿을 복사해서 위에 붙여넣으세요 -->
<!--
## [YYYY-MM-DD] Session N — 제목

### 사용자 요청

> 요청 내용 원문 또는 요약

### 변경 사항

| 파일 | 동작 | 설명 |
|------|------|------|
| `파일명` | 신규/수정/삭제 | 설명 |

### 주요 결정 사항

- 결정 이유와 배경
-->
