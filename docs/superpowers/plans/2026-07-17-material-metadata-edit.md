# Material Metadata Edit Documentation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Notion 기능 명세서, Figma PM 와이어프레임, 로컬 docs의 자료 수정·검토 계약을 컴팩트 모달 확정안으로 일치시킨다.

**Architecture:** `UPL001` 대기열의 본인 자료에서만 `자료 수정`을 제공하고, `UPL001-0200` 컴팩트 모달에서 자료 제목과 자료 설명만 수정한다. `REV001`은 검토 필요 자료의 최초 검토만 제공하며 `검토 마치기` 후 본인 검토 결과 재수정은 제공하지 않는다. 기능 ID는 유지하고 파생 화면 ID만 추가한다.

**Tech Stack:** Markdown, Notion MCP, Figma Plugin API

## Global Constraints

- 문서 용어는 `자료 설명`을 유지한다.
- 자료 제목과 자료 설명만 수정하며 파일·본문·주차·업로더·AI 결과는 수정하지 않는다.
- 대기열에 존재하는 동안 본인 자료만 수정할 수 있다.
- `검토 마치기` 제출 후 검토 결과 재수정은 제공하지 않는다.
- 업로드 주차 선택 UI는 다시 추가하지 않는다.
- 데모 코드는 수정하지 않는다.
- 사용자 요청이 없으므로 커밋하지 않는다.

---

### Task 1: 로컬 문서 계약 정합화

**Files:**
- Create: `docs/변경사항/합의_0717_자료수정.md`
- Modify: `docs/화면설계서.md`
- Modify: `docs/wire_frame_requirements/00-index.md`
- Modify: `docs/wire_frame_requirements/02-home.md`
- Modify: `docs/wire_frame_requirements/04-study-upload.md`
- Modify: `docs/wire_frame_requirements/09-review-screen.md`
- Modify: `AGENTS.md`
- Modify: `docs/AGENTS.md`

**Interfaces:**
- Consumes: `UPL001`, `REV001`, `HOM001-0400`, `STD-UP-LIST-01`, `REV-ENT-01`, `REV-SUB-01`, `HOME-ACT-01`
- Produces: `UPL001-0200 자료 수정 모달`과 검토 재수정이 제거된 최신 계약

- [ ] 기존 `수정하기` 문장을 검토 재진입 의미와 질문함 수정 의미로 구분한다.
- [ ] 업로드 명세에 제목·자료 설명만 편집하는 `UPL001-0200` 모달을 추가한다.
- [ ] 검토·홈 최신 명세에서 검토 결과 재수정 상태와 CTA를 제거한다.
- [ ] `rg -n "본인 검토 변경|검토 화면 재진입|UPL001-0200|자료 설명" docs`로 잔존 문구와 새 계약을 확인한다.

### Task 2: Figma PM 와이어프레임 최신화

**Files:**
- Update external: Figma `Stology_PM_Wireframe` / `Stology PM Wireframe Spec v2`

**Interfaces:**
- Consumes: 기존 `05. 자료 업로드 UPL001`, `05-02. 대기 자료 상태 UPL001`, `06-03. 검토 완료 분기 REV001`, `02-09. 자료 상세 HOM001-0400`
- Produces: `05-06. 자료 수정 모달 UPL001-0200`과 최신 Description·사용자 플로우

- [ ] 기존 프레임의 레이어 구조, 텍스트 스타일, Callout/Description 패턴을 검사한다.
- [ ] `05. 자료 업로드 UPL001`과 `05-02`에서 검토 재진입 의미의 `수정하기`를 `자료 수정` 또는 검토 대기 상태로 교체한다.
- [ ] 컴팩트 모달 파생 프레임을 만들고 제목·자료 설명·취소·저장만 표시한다.
- [ ] `06-03`에서 인원 미충족 시 본인 재수정 분기를 다른 멤버 검토 대기로 교체한다.
- [ ] `HOM001-0400`에서 `수정하기` 검토 CTA를 제거한다.
- [ ] 스크린샷과 자동 점검으로 텍스트 잘림, Callout/Description 불일치, 모달 가독성을 확인한다.

### Task 3: Notion 기능 명세 최신화

**Files:**
- Update external: Notion `📘 3. 스터디 페이지`
- Update external: Notion `🏠 2. 홈 화면`
- Update external: Notion `✅ 4. AI 추출 결과 검토 화면 (1)`

**Interfaces:**
- Consumes: 로컬 합의 문서의 최신 계약
- Produces: 동일 기능 ID를 유지하면서 구계약만 교체된 Notion 기능 명세

- [ ] `STD-UP-LIST-01`을 본인 대기 자료의 제목·자료 설명 수정 계약으로 교체한다.
- [ ] `HOME-ACT-01`의 검토 집계에서 `수정하기`를 제거한다.
- [ ] `REV-ENT-01`, `REV-ACT-01`, `REV-SUB-01`을 제출 후 변경 불가 계약으로 교체한다.
- [ ] 세 페이지를 다시 fetch해 구계약이 제거됐는지 확인한다.

### Task 4: 최종 정합성 검증

**Files:**
- Verify: Tasks 1–3 산출물

**Interfaces:**
- Consumes: 로컬 docs, Figma, Notion 최신 결과
- Produces: 용어·기능 ID·화면 ID 정합성 확인 결과

- [ ] 로컬 최신 명세에서 검토 재진입 문구가 제거됐는지 검색한다.
- [ ] Notion의 세 기능 ID가 로컬 문서와 같은 정책인지 확인한다.
- [ ] Figma의 `UPL001-0200` 및 관련 프레임 문구가 같은 정책인지 확인한다.
- [ ] `git diff --check`로 로컬 문서 형식 오류를 확인한다.
