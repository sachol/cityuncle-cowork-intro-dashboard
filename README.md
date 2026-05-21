# 공인중개사 5분 입문 — Claude Cowork 가이드 대시보드

> **gpters 22기 W1 미니 사례** · 2026-05-20 (수) 작성 · 2026-05-21 검증·정정 1차
> 단일 정적 HTML 페이지 · Tailwind CDN · 라이트/다크 모드 · Cowork Dispatch(베타) 시연

---

## 무엇을 만들었나

공인중개사가 **5분 안에 Claude Cowork을 따라할 수 있는 1페이지 가이드 대시보드**.

- 설치(Claude Desktop) → "내 부동산 사무소" Project → 첫 프롬프트 3단계
- 매물 분석·광고·카톡 응대·보고서 4가지 진입점
- **Dispatch (베타) 시연** — Cowork 공식 기능. 📱 폰에서 보내면 → 💻 사무소 컴퓨터가 처리 → 📲 폰으로 결과. 외근·임장 중에 사무소 컴퓨터에 일을 시키는 패턴.
- 라이트/다크 토글 (CSS 변수 + localStorage + prefers-color-scheme)
- 네오브루탈리즘 + 키네틱 타이포 + 그라데이션 메쉬 융합 디자인

---

## 파일 구조

```
cowork-intro-dashboard/
├─ index.html       # 최종 결과물 (브라우저로 바로 열기)
├─ content.md       # 카피 원본 (강의·블로그 재사용용) + 디자인 토큰
├─ plan.md          # 이 서브 프로젝트 plan (4시간 분할)
├─ AGENTS.md        # sub-agent 3종 정의 (cowork-curator / realtor-copy-writer / neobrutal-designer)
├─ README.md        # 본 문서
└─ assets/          # 이미지·아이콘
```

---

## 미리보기 방법

### 1️⃣ 가장 빠른 방법 — 더블클릭
`index.html` 파일을 **더블클릭** → 기본 브라우저에서 즉시 열림.

### 2️⃣ 로컬 서버 (권장, 폰트 CDN이 안정적)
PowerShell에서:
```powershell
cd c:\Users\pc\gpters22_edu\subprojects\cowork-intro-dashboard
python -m http.server 8765
```
브라우저에서 http://localhost:8765 열기.

### 3️⃣ 모바일 미리보기
Chrome DevTools (F12) → 좌측 상단 디바이스 아이콘 → iPhone SE / iPad / Galaxy S20 등 선택.

---

## 작동하는 인터랙션 4종

| 인터랙션 | 어디 | 동작 |
|---|---|---|
| 키네틱 타이포 | 6개 섹션 H2 헤딩 | 마우스 호버 시 살짝 흔들림 |
| 사례 카드 펼침 | CASE 01~03 | 카드 클릭 시 Before/After 펼침 |
| **Dispatch (베타) 시연** ⭐ | CASE 04 (검정 배경) | 📱→💻→📲 3단 흐름 시각화 + 폰 입력 예시 + `▶ 폰에서 한 줄 보내기` 클릭 시 데스크탑이 만들어내는 4개 산출물 시간차 등장 + 각 카드의 "데스크탑이 받은 지시 보기" 펼침 |
| 체크리스트 | NEXT 섹션 | 체크박스 클릭 시 ✓ 표시 + 취소선 |

---

## 게시판 공유용 글 (200~300자, 복사해서 그대로 쓰세요)

> **공인중개사 5분 입문 — Claude Cowork으로 사무소 업무 반으로 줄이기 🏢**
>
> gpters 22기 오리엔테이션 전에, 제가 강의에서 다루는 도구 중 하나인 **Claude Cowork**(Anthropic의 데스크탑 앱 전용 AI 워크스페이스)을 공인중개사 입장에서 따라하기 쉽게 정리한 1페이지 가이드를 만들었습니다.
>
> ✅ Claude Desktop 설치부터 첫 결과물까지 약 10분
> ✅ 매물 분석·광고·카톡 응대·보고서 4가지 진입점
> ✅ Cowork **Dispatch (베타)** 시연 — 📱 폰으로 한 줄 보내면 → 💻 사무소 컴퓨터가 처리 → 📲 폰으로 결과 (임장·외근 중 강력)
>
> 강사가 본인 강의에 그대로 쓰는 자료라, 공인중개사가 아니어도 "AI 도구를 어떻게 도메인에 끼우는지" 사례로 보실 수 있습니다.
>
> 👉 [대시보드 링크]
>
> 피드백·질문 환영합니다. 도시아재 드림 🙌

---

## 디자인 시스템 한눈에

| 토큰 | 값 | 어디 |
|---|---|---|
| `--ink` | `#0A0A0A` | 외곽선·본문 |
| `--paper` | `#FFFCEF` | 배경 |
| `--yellow` | `#FFD600` | Hero·CTA·강조 |
| `--pink` | `#FF4D8D` | CASE 03 카드·CTA |
| `--mint` | `#A7F3D0` | Dispatch 산출물 A 카드·체크 완료 |
| `--purple` | `#C4B5FD` | Dispatch 산출물 D 카드 |
| shadow | `8px 8px 0 var(--ink)` | 큰 카드 |
| shadow-sm | `4px 4px 0 var(--ink)` | 작은 카드 |
| border | `3px solid var(--ink)` | 모든 카드·버튼 |
| radius | `20px` | 카드 모서리 |

폰트: Pretendard Variable (헤딩 900 / 본문 500) · JetBrains Mono (프롬프트 예시)

---

## 다음 단계 (이 사례 자체의)

| 시점 | 할 일 |
|---|---|
| 오늘 | 로컬 미리보기 → 6 섹션 모두 렌더링 확인 → 메인에 커밋 |
| 5/21~22 | 카피 다듬기 (강사 본인 어조로 한 번 더 패스) |
| 5/22~23 | 호스팅 결정 (GitHub Pages 또는 Vercel) 후 배포 |
| 5/23 (토) OT 전 | 게시판 글 + 링크 + 썸네일 1장 업로드 |

---

## 강의에 어떻게 쓰나

이 페이지는 **강의 도입 자료**입니다:

1. **오프닝 5분**: 학생들에게 이 페이지 링크 전달 → 따라하기 체크리스트 채우게 하기
2. **본 강의 진입**: "이 4가지 진입점 중 어떤 게 가장 도움 될 것 같으세요?" 발문
3. **사례 시연**: Dispatch (베타) 시연 카드를 화면 공유 → 실제 Cowork Dispatch 사용법(폰↔데스크탑) 설명
4. **마무리**: NEXT 섹션의 "일주일 후 / 한 달 후"로 학습 동기 부여

---

## 부수 효과 — 메인-서브 프로젝트 구조의 첫 번째 사례

이 서브 프로젝트는 **`subprojects/<name>/`** 패턴을 처음 도입한 사례입니다.
W1 본 사례(`property-360-report`), W2 Cowork 강의자료, W3 대시보드, W4 크롬 확장도 모두 같은 구조로 정리될 예정.

자세한 거버넌스는 [`AGENTS.md`](./AGENTS.md) 마지막 섹션 참조.
