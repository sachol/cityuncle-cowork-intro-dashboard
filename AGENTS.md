# AGENTS — cowork-intro-dashboard 서브 프로젝트

> 이 파일은 **서브 프로젝트 로컬 agent 정의서**입니다.
> 글로벌 `~/.claude/agents/`에는 두지 않고, 이 서브 프로젝트 안에서만 의미를 갖습니다.
> 메인-서브 거버넌스 검증용 — 향후 W1~W4 사례 모두 이 패턴을 따릅니다.

---

## 정의된 agent (3종)

### 1. `cowork-curator`
**역할**: Claude Cowork(claude.ai의 Projects/협업 워크스페이스) 공식 문서·블로그·릴리스 노트를 읽고, **공인중개사 도메인에 맞는 사용 사례로 번역**.

**입력**: 공식 docs URL, 기능 이름(예: "System Instructions", "Projects", "Artifacts", "Files")
**출력**: 공인중개사 1인 사무소가 즉시 따라할 수 있는 **3줄짜리 한국어 사용 사례**

**언제 호출**: 새 Cowork 기능이 릴리스되었을 때, 또는 강의 자료에 사례 1줄 추가할 때.

**Do NOT 사용 케이스**:
- 코드 구현 (정적 페이지나 강의 자료 외)
- 외부 API 호출이 필요한 작업
- 부동산 시세·등기 등 도메인 데이터 분석 (그건 `property-360-report` 영역)

---

### 2. `realtor-copy-writer`
**역할**: 전문 IT 용어를 최소화하고, **카톡으로 그대로 보낼 수 있는 친근체** 한국어 카피 작성.

**입력**: 기능 설명 또는 사례 outline (영문·한자 섞여 있어도 OK)
**출력**:
- 헤딩 1줄 (8~14자, 강한 동사 포함)
- 본문 2~3줄 (구체 숫자 1개 이상 포함)
- 한 줄 CTA

**스타일 가이드**:
- "AI를 활용한 매물 분석 자동화 솔루션" ❌
- "주소 한 줄 넣으면 시세 정리 끝" ✅
- 영문 용어는 한국어 + 짧은 영문 병기 ("프로젝트(Project)")
- 부정문 최소화, 행동 동사 우선

---

### 3. `neobrutal-designer`
**역할**: 네오브루탈리즘 + 최신 트렌드 융합 디자인 토큰·CSS 스니펫 생성.

**입력**: 컴포넌트 이름 (카드, 버튼, 입력창, 배지 등)
**출력**: 다음 4가지를 모두 포함한 CSS 스니펫
1. `border: 3px solid var(--ink)` 외곽선
2. `box-shadow: Nx Nx 0 var(--ink)` 오프셋 그림자
3. `:hover` 시 transform translate + 그림자 증가
4. `:active` 시 transform 반대로 + 그림자 감소

**금지**:
- 미니멀리즘·머티리얼·Apple Liquid Glass 등 다른 디자인 언어 혼용
- 그라데이션 (Hero 메쉬 배경 1곳 외 사용 금지)
- 둥근 모서리 16~20px 외 다른 값

---

## 구현 상태

| Agent | 정의 | 실제 구현 | 사용된 곳 |
|---|---|---|---|
| `cowork-curator` | ✅ 본 문서 | ❌ 아직 미구현 (오늘은 inline으로 처리) | content.md ②·④·⑤ |
| `realtor-copy-writer` | ✅ 본 문서 | ❌ 아직 미구현 (오늘은 inline) | content.md 전반 |
| `neobrutal-designer` | ✅ 본 문서 | ❌ 아직 미구현 (오늘은 inline) | content.md 디자인 토큰 + index.html `<style>` |

**오늘 결정**: 시간 압축으로 3 agent 모두 **정의만** 두고 실제 `.md` agent 파일은 만들지 않음.
다음 사례(W1 본 사례 `property-360-report`)에서 첫 번째 agent를 실제로 만들어 패턴 검증.

---

## 메인-서브 거버넌스 메모

이 서브 프로젝트가 가지는 **로컬 자원**:
- `plan.md` — 이 서브 프로젝트만의 plan
- `content.md` — 카피 원본
- `AGENTS.md` — 이 파일 (로컬 agent 정의)
- `index.html` — 결과물
- `README.md` — 공유용 안내
- `assets/` — 이미지

**메인(`gpters22_edu`)에서 끌어 쓰는 것**:
- 글로벌 CLAUDE.md (강의 철학·도메인 컨텍스트)
- Notion DB ID (db-registry.json)
- 글로벌 스킬 (`design-html`, `gstack`, `checkpoint` 등)

**서브가 메인으로 올리는 것** (선택적):
- 검증된 패턴 → 메인의 `docs/00-curriculum.md`에 사례 카드로 인덱싱
- 재사용 가능한 agent 정의 → 글로벌 `~/.claude/agents/`로 승격 검토

---

## 다음 사례를 위한 체크리스트

다음 W1~W4 서브 프로젝트를 시작할 때, 이 문서를 템플릿 삼아 다음을 채울 것:

- [ ] 도메인 특화 agent 2~3개 정의 (역할·입력·출력·금지)
- [ ] 메인에서 끌어 쓰는 것 vs 서브 로컬 자원 명확히 구분
- [ ] 정의만 두고 실제 구현은 첫 사용처에서 시작 (오버 엔지니어링 방지)
