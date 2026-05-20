# Plan — 공인중개사용 Claude Cowork 가이드 대시보드 (W1 미니 사례)
> 작성 시점: 2026-05-20 (수) W1 본 수업 중
> 작성 위치: `C:\Users\pc\.claude\plans\rippling-booping-seahorse.md`

---

## 1. Context — 왜 만드는가

신화 대표님은 gpters 22기 W1 본 수업 중 **두 가지 결정**을 내림:

1. **(장기)** `gpters22_edu`를 **메인 프로젝트**로 두고, 매주 사례(W1~W4)는 **서브 프로젝트**로 분리. 각 서브 프로젝트는 자체 agent/sub-agent를 가짐.
2. **(즉시 / 이번 plan의 본체)** 수업 후 3~4시간 안에 **공인중개사용 Claude Cowork 가이드 대시보드** 미니 사례를 만들어 **2026-05-23(토) OT 전 클래스 게시판에 공유**.

이 미니 사례는 통합 스토리("주소 한 줄 → 영업 한 세트")와 **독립**이며, 다음을 동시에 충족해야 함:
- **수강 대상자(공인중개사)가 따라하기 쉬워야 함** — 복잡하지 않게.
- **교육자(신화 대표님) 입장에서 즉시 강의에 투입 가능한 자원**.
- **만드는 과정 자체가 교육 사례** — 강의·게시판에서 "이렇게 만들었다" 흐름을 시연.
- **본인 미적 취향(네오브루탈리즘) + 최신 디자인 트렌드** 결합.
- **dispatch 기능 데모 포함** (Claude Code의 멀티 에이전트 분기 실행을 공인중개사 업무 사례에 빗대 시뮬레이션).

---

## 2. 결과물 사양

### 2.1 정체성
| 항목 | 결정 |
|---|---|
| 코드명 | `cowork-intro-dashboard` |
| 한국어 제목(가안) | "공인중개사 5분 입문 — Claude Cowork으로 사무소 일 절반으로 줄이기" |
| 대상 | 공인중개사·중개보조원 (gpters 비수강생 포함, 누구나 처음 열어도 OK) |
| 톤 | 친절·구체·실용. 전문 용어는 한국어 + 짧은 영문 병기 |
| 결과물 형태 | **단일 정적 HTML 페이지** (스크롤형 대시보드) |
| 호스팅 | 1차: 로컬 미리보기 → 2차: GitHub Pages 또는 Vercel (작업 중 결정) |
| 마감 | 2026-05-23 (토) OT 전 |

### 2.2 콘텐츠 구조 (6 섹션)

```
[Hero]      → "공인중개사도 5분이면 시작" + 짧은 미션 한 줄
[What]      → Claude Cowork이란? (3개 핵심 강점 카드)
[How]       → 사용 방법 3단계 (가입 → 첫 프롬프트 → 결과 확인)
[Apply]     → 공인중개사 워크플로우에 끼우는 4가지 진입점
              (매물 분석 / 광고문 / 카톡 응대 / 보고서)
[Cases]     → 추천 사례 카드 4~6장 (인터랙티브 + dispatch 데모 1개)
[Next]      → "직접 따라하기" 체크리스트 + 강의 안내 CTA
```

### 2.3 dispatch 데모 (인터랙티브 핵심)

**시나리오**: 사용자가 "광화문 X마을 4단지 시세·시장 분석"을 입력 → 버튼 클릭 → 화면에 **4개 워커가 동시 분기**되어 작업하는 모습을 시뮬레이션:

```
입력: "광화문 X마을 4단지"
   │
   ├─ 워커 A: 실거래가 분석   → 결과 카드 슬라이드 인
   ├─ 워커 B: 광고 카피 초안  → 결과 카드 슬라이드 인
   ├─ 워커 C: 카톡 응대 초안   → 결과 카드 슬라이드 인
   └─ 워커 D: 고객 보고서 초안 → 결과 카드 슬라이드 인
```

- 실제 API 호출 없음 — **하드코딩된 가상 결과**를 시간차로 펼침 (CSS 트랜지션 + setTimeout).
- 4개가 **병렬로** 풀려나가는 시각 효과가 핵심 (dispatch=동시 작업 분기의 메타포).
- 카드 클릭하면 "이건 실제로는 이런 명령으로 만들어집니다" Cowork 프롬프트 예시를 펼침.

### 2.4 디자인 방향

**기본 골격**: **네오브루탈리즘**
- 굵은 검정 외곽선(2~4px), 두꺼운 오프셋 그림자(8px 4px 0 #000)
- 원색 톤: 노랑(#FFD600) · 검정 · 흰색 · 핑크 액센트(#FF4D8D)
- 비대칭 그리드, 거친 정렬

**최신 트렌드 결합 (2개만 선별)**:
1. **키네틱 타이포** — 헤딩 호버 시 살짝 떨림·뒤집힘 (CSS transform)
2. **그라데이션 메쉬 배경** — Hero 섹션 한정, 네오브루탈 카드와 대비

**폰트**:
- 헤딩: **Pretendard Black 900** (한국어 가독성)
- 본문: Pretendard 400/500
- 모노스페이스(코드/프롬프트 예시): JetBrains Mono 또는 Fira Code

---

## 3. 기술 스택 & 파일 구조

### 3.1 스택 (최소 의존)
| 영역 | 선택 | 이유 |
|---|---|---|
| HTML | 단일 `index.html` | 호스팅 간단·수정 직관적 |
| CSS | Tailwind CDN | 빠르게, 빌드 없음 |
| JS | Vanilla JS (또는 Alpine.js CDN) | dispatch 데모 인터랙션만 필요 |
| 폰트 | Pretendard CDN | 한국어 |
| 아이콘 | Lucide CDN 또는 Heroicons inline SVG | 네오브루탈과 어울리는 단색 라인 |

> 빌드 도구 없음. 파일 더블클릭 또는 `python -m http.server`로 즉시 미리보기.

### 3.2 파일 구조 (새로 만들 폴더)

```
c:\Users\pc\gpters22_edu\
  subprojects\                          # NEW — 서브 프로젝트 표준 위치
    cowork-intro-dashboard\             # 이번 미니 사례
      index.html                        # 메인 결과물
      content.md                        # 카피 원본 (HTML과 분리해서 강의용으로 재사용)
      plan.md                           # 이 서브 프로젝트의 plan (이 파일에서 옮겨옴)
      AGENTS.md                         # 이 서브 프로젝트의 custom agent 정의
      README.md                         # 공유용 안내문 (게시판에 그대로 붙여넣을 수 있는 형태)
      assets\                           # 이미지·아이콘
        og-cover.png                    # 게시판 썸네일
```

**`subprojects/` 도입 의의**: 향후 W1~W4 사례도 같은 패턴으로 자리 잡힘. 메인-서브 분리의 첫 발.

---

## 4. 작업 단계 (3~4시간 분할)

| T | 단계 | 산출 |
|---|---|---|
| T+0:00 ~ 0:30 | **콘텐츠 outline + 핵심 카피** | `content.md` (6섹션 마크다운, 한국어 카피 확정) |
| T+0:30 ~ 1:00 | **디자인 토큰 결정** (컬러·폰트·그림자·간격) | content.md 상단에 토큰 표 |
| T+1:00 ~ 2:00 | **`index.html` 정적 마크업** (6섹션 모두) | 인터랙션 없는 완전한 정적 페이지 |
| T+2:00 ~ 3:00 | **dispatch 데모 인터랙션 구현** | 4-워커 시뮬레이션 작동, 카드 클릭 펼침 |
| T+3:00 ~ 3:30 | **QA & 다듬기** (브라우저, 모바일 뷰포트, 카피 교정) | 결정한 호스팅에 배포 |
| T+3:30 ~ 4:00 | **README + 게시판용 공유글 + 커밋** | 게시판에 붙여넣을 수 있는 200~300자 글 |

각 단계 끝에 **`checkpoint` 스킬로 진행 저장** → 중간에 멈춰도 복구 쉬움.

---

## 5. 활용 스킬·에이전트

### 5.1 활용할 기존 스킬 (재사용 우선)
| 스킬 | 단계 | 용도 |
|---|---|---|
| `superpowers:brainstorming` | T+0:00 | 6 섹션 후크·카피 후보 발산 |
| `design-html` 또는 `design-consultation` | T+0:30 | 네오브루탈+트렌드 융합 디자인 시스템 한 줄 결정 |
| `frontend-design` (또는 직접) | T+1:00 | Tailwind 마크업 구조화 |
| `gstack` / `browse` | T+3:00 | QA 스크린샷 (모바일·데스크탑) |
| `checkpoint` | 각 단계 | 진행 저장 |

### 5.2 새로 만들 sub-agent (옵션 — 본 작업 중 결정)

`subprojects/cowork-intro-dashboard/AGENTS.md`에 정의 (글로벌 `.claude/agents/`에는 안 두고 로컬 보관 → 서브 프로젝트 컨셉 검증):

| 이름 | 역할 |
|---|---|
| `cowork-curator` | Claude Cowork 공식 docs 읽고 공인중개사용 사례로 변환 |
| `realtor-copy-writer` | 전문 용어 최소화, 카톡톤 친근체 카피 작성 |
| `neobrutal-designer` | 디자인 토큰·CSS 스니펫 생성 |

> **결정**: 시간 부족하면 이 3 agent는 다음 사례에서 도입. 오늘은 inline으로 처리.

---

## 6. 메인-서브 프로젝트 거버넌스 (별도 트랙)

오늘 plan의 **부수 효과**로 `subprojects/cowork-intro-dashboard/`가 처음 만들어지며, 이것이 향후 표준이 됨:

```
gpters22_edu/                        # 메인 (전체 강의 운영 자동화)
  .claude/                           # 메인 공통 설정·전역 agent
  docs/                              # 메인 커리큘럼·핸드오프
  notion-sync/                       # 메인 운영 인프라
  subprojects/                       # 매주 사례 서브 프로젝트
    cowork-intro-dashboard/          # (오늘 NEW)
    property-360-report/             # → 향후 W1 본 사례 (현재 .claude/skills/에 있음, 이동 검토)
    listing-to-sns/                  # → 향후 W1 백업 사례
    (W2, W3, W4 사례들…)
```

**오늘 plan에 포함되지 않는 것** (다음 plan에서 다룸):
- 기존 `.claude/skills/property-360-report/` 등을 `subprojects/`로 마이그레이션
- 글로벌 agent와 sub-project agent 경계 설계
- 메인-서브 간 데이터 공유 규칙 (예: Notion DB 접근권)

---

## 7. 검증 방법 (End-to-End)

1. **로컬 미리보기**: `subprojects/cowork-intro-dashboard/index.html` 더블클릭 → 6섹션 모두 렌더 확인.
2. **반응형 체크**: Chrome DevTools에서 375px(iPhone SE) · 768px(태블릿) · 1280px(데스크탑) 3개 뷰포트.
3. **dispatch 데모 작동**: 입력 → 버튼 클릭 → 4개 워커 카드 순차/병렬 풀림 확인. 카드 클릭 시 프롬프트 예시 펼침 확인.
4. **카피 검수**: 공인중개사가 처음 봐도 막힘없이 읽히는지. 모든 영문 용어는 한국어 병기.
5. **링크 검수**: Cowork 공식 페이지·강의 신청 CTA 링크 4xx/5xx 없음.
6. **(선택) `gstack`/`browse`로 자동 스크린샷**: 데스크탑·모바일 PNG 저장 → `assets/`에 보관, 게시판 글에 첨부.
7. **공유**: 게시판 글 200~300자 카피 + 대시보드 링크 + 썸네일 이미지 1장 → gpters 22기 게시판 업로드.

---

## 8. 위험·결정 보류 사항

| 항목 | 처리 |
|---|---|
| "Cowork의 dispatch 기능"의 정확한 정의 | 작업 시작 시 1차로 공식 docs 확인. 모호하면 **"여러 작업을 동시에 분배"**라는 메타포로 일반화. |
| 호스팅 결정 (GitHub Pages vs Vercel) | T+3:00 시점에 신화 대표님께 짧게 확인. 디폴트는 GitHub Pages. |
| Sub-agent 3종 실제로 만들지 | 시간 봐서. 못 만들면 inline 처리하고 plan만 `AGENTS.md`에 적어 둠. |
| 토요일까지 폴리시 여유 | 오늘 MVP까지 + 목·금에 카피 다듬기 가능 (이 plan은 오늘만 다룸). |

---

## 9. 오늘 plan의 산출물 (커밋 단위)

수업 후 작업이 끝났을 때 다음 커밋이 있어야 함:

```
feat(subprojects): cowork-intro-dashboard 미니 사례 신설
  - subprojects/cowork-intro-dashboard/index.html
  - subprojects/cowork-intro-dashboard/content.md
  - subprojects/cowork-intro-dashboard/plan.md (이 plan을 옮겨옴)
  - subprojects/cowork-intro-dashboard/README.md
  - subprojects/cowork-intro-dashboard/AGENTS.md (정의만, 미구현 OK)
  - subprojects/cowork-intro-dashboard/assets/og-cover.png
docs(handoff): HANDOFF.md에 W0 미니 사례 신설·게시판 공유 진행 상태 반영
```

> 별도로, **현재 작업 트리에 미커밋 상태인 `docs/intro/zoom-intro-w1.md` 변경분**(③ 단락 능동 톤 재작성 + 채팅용 4항목)이 남아 있음. 작업 시작 전 그것부터 먼저 커밋.

---

## 10. 최우선 다음 액션 (수업 끝나는 23:00 이후)

1. 미커밋 상태 `zoom-intro-w1.md` 먼저 커밋 (별건이라 분리).
2. `subprojects/cowork-intro-dashboard/` 디렉토리 생성 + 이 plan을 `plan.md`로 복사.
3. T+0:00 단계(`content.md` outline) 시작.
