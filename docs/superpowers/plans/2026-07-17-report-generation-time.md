# Report Generation Time Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 시작일 기반 주차 종료 요일과 리포트 자동 생성 시각 정책을 Notion, 로컬 기능명세, Figma 화면설명에 동일하게 반영한다.

**Architecture:** `HOME-CRT-01`이 시작일과 기본 일정을 확정하고, `STD-MGT-03`이 생성 후 시각 수정과 적용 예약을 소유한다. `RPT-WEEK-01`은 확정된 종료 시각을 완료 주차 판단과 자동 생성 트리거로 사용한다.

**Tech Stack:** Markdown, Notion 기능 명세서, Figma Plugin API

## Global Constraints

- 기준 시간대는 `Asia/Seoul`이다.
- 시작일의 전날을 종료 요일로 고정하고 기본 시각은 `24:00`으로 표시한다.
- 생성 후에는 종료 요일을 바꾸지 않고 시각만 수정한다.
- 시작 후 변경은 다음 주차부터 적용하며 완료 리포트는 재계산하지 않는다.
- 사용자 요청 없이 Git 커밋하지 않는다.

---

### Task 1: 합의 및 로컬 화면 계약

**Files:**
- Create: `docs/변경사항/합의_0717_리포트생성시간.md`
- Modify: `docs/기획안.md`
- Modify: `docs/화면설계서.md`
- Modify: `docs/wire_frame_requirements/00-index.md`
- Modify: `docs/wire_frame_requirements/02-home.md`
- Modify: `docs/wire_frame_requirements/06-study-report.md`
- Modify: `docs/wire_frame_requirements/07-study-container.md`
- Modify: `AGENTS.md`

- [x] 시작일 기반 종료 요일, 기본 24:00, KST, 변경 적용 시점을 같은 용어로 반영한다.
- [x] `MGT001-0200`과 `STD-MGT-03` 추적성을 추가한다.
- [x] `rg`로 화면 ID, 기능 ID, 24:00, 다음 주차 적용 문구를 교차 검증한다.

### Task 2: Notion 기능 명세서

**External target:**
- `기능 명세서 / 🏠 2. 홈 화면`
- `기능 명세서 / 📘 3. 스터디 페이지`

- [x] `HOME-CRT-01`에 시작일 기반 기본 일정과 생성 후 잠금 정책을 반영한다.
- [x] `STD-MGT-01` 설정 메뉴에 리포트 생성 시간 진입점을 추가한다.
- [x] `STD-MGT-03` 기능 블록을 추가한다.
- [x] `RPT-WEEK-01`에 주차 종료 판단과 자동 생성 트리거를 반영한다.

### Task 3: Figma 기능명세

**External target:** `Stology_PM_Wireframe / Stology PM Wireframe Spec v2`

- [x] `02-02. 스터디 생성 HOM001-0100`에 기본 일정 안내와 Description을 반영한다.
- [x] `03-01. 설정 드롭다운 MGT001`에 `리포트 생성 시간` 항목과 기능 ID를 반영한다.
- [x] `03-07. 리포트 생성 시간 MGT001-0200` 파생 프레임을 추가한다.
- [x] `08. 주차별 리포트 RPT001` Description에 설정 일정 기반 완료/자동 생성 정책을 반영한다.
- [x] 메타데이터와 스크린샷으로 프레임명, Description, 텍스트 가림을 검증한다.
