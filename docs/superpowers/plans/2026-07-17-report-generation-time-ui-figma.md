# Report Generation Time UI Figma Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** `03-07. 리포트 생성 시간 MGT001-0200`을 정보 표시 화면에서 실제 시·분 드롭다운을 가진 설정 UI로 수정한다.

**Architecture:** 기존 PM 와이어프레임 프레임과 모달 구조는 유지하고, 일정 정보 나열 영역을 읽기 전용 종료 요일, 시·분 드롭다운, 적용 미리보기로 재구성한다. 새 화면 ID를 만들지 않고 Description과 콜아웃을 동일 프레임에서 갱신한다.

**Tech Stack:** Figma Design, Figma Plugin API, `figma-use`, PM 와이어프레임 Description/Callout 규칙

## Global Constraints

- 대상 파일 키는 `SSCK0wKWEc943emer8VNnJ`이다.
- 대상 프레임은 `1723:52`, 이름은 `03-07. 리포트 생성 시간 MGT001-0200`이다.
- 종료 요일은 `매주 화요일`, 보조 문구는 `시작일 기준 · 변경 불가`로 표시한다.
- 시간 옵션은 `00시–24시`, 분 옵션은 `00·10·20·30·40·50분`이다.
- `24시` 선택 시 `00분`으로 고정하고 분 드롭다운을 비활성화한다.
- 기준 시간대는 `Asia/Seoul`이다.
- 현재 주차와 다음 주차 적용 일정을 분리해 표시한다.
- 새 화면 ID를 추가하지 않는다.
- 사용자 요청 없이 Git 커밋하지 않는다.

---

### Task 1: 모달 입력 영역 재구성

**External target:**
- Modify: Figma file `SSCK0wKWEc943emer8VNnJ`, frame `1723:52`

**Interfaces:**
- Consumes: `docs/superpowers/specs/2026-07-17-report-generation-time-ui-design.md`
- Produces: 시·분 드롭다운과 적용 미리보기가 포함된 `MGT001-0200` 기본 상태

- [x] **Step 1: 기존 프레임과 텍스트 폰트 확인**

  `1723:52`의 모달 카드, 제목, 필드, 버튼, Description, Callout 노드 ID를 조회한다. 수정할 모든 TEXT 노드의 현재 `fontName` 세그먼트를 읽고 `figma.loadFontAsync`로 로드한다.

- [x] **Step 2: 종료 요일 읽기 전용 영역 구성**

  기존 일정 정보 박스를 `종료 요일`, `매주 화요일`, `시작일 기준 · 변경 불가` 구조로 바꾼다. 종료 요일 영역은 중립 배경과 테두리를 사용해 입력 불가 상태로 표현한다.

- [x] **Step 3: 시·분 드롭다운 구성**

  `생성 시간` 레이블 아래에 `21시 ⌄ : 20분 ⌄` 형태의 두 드롭다운을 배치한다. 하단에 `10분 단위 · Asia/Seoul` 보조 문구를 표시한다. Figma 기본 상태는 닫힌 드롭다운으로 표현한다.

- [x] **Step 4: 적용 미리보기 구성**

  강조 박스에 다음 세 줄을 표시한다.

  ```text
  현재 3주차 · 화요일 24:00 유지
  4주차부터 · 화요일 21:20
  다음 리포트 · 7월 28일 화요일 24:00
  ```

  두 번째 줄을 강조하고 `저장하면 이렇게 적용돼요` 제목을 표시한다.

- [x] **Step 5: 버튼 상태 유지**

  하단 `취소`와 Primary `저장` 버튼을 유지하고 입력 영역과 겹치지 않게 정렬한다.

### Task 2: 기능명세 Description 갱신

**External target:**
- Modify: Figma file `SSCK0wKWEc943emer8VNnJ`, frame `1723:52`

**Interfaces:**
- Consumes: Task 1의 입력 UI
- Produces: UI와 일치하는 4개 Description 및 4개 Callout

- [x] **Step 1: Description 네 항목 수정**

  ```text
  1. 종료 요일은 시작일 전날로 고정하고 생성 시각만 수정한다. 관련 기능 ID: STD-MGT-03
  2. 시간은 00–24시, 분은 10분 단위다. 24시 선택 시 00분으로 고정하고 분 선택을 비활성화한다.
  3. 시작 전 변경은 1주차부터, 시작 후 변경은 다음 주차부터 적용한다.
  4. 완료 리포트는 변경하지 않고 예약 재수정은 마지막 저장값으로 교체한다.
  ```

- [x] **Step 2: Callout 대응 확인**

  Callout 1–4를 각각 제목/종료 요일, 시·분 입력, 적용 미리보기, 저장 액션에 대응시킨다. 모든 Callout 컨테이너는 대상 프레임의 직접 자식이며 잠금 해제 상태여야 한다.

### Task 3: Figma 검증

**External target:**
- Read: Figma file `SSCK0wKWEc943emer8VNnJ`, frame `1723:52`

**Interfaces:**
- Consumes: Task 1–2 결과
- Produces: 구조·문구·시각 QA 결과

- [x] **Step 1: 문자열 자동 검증**

  프레임 내 TEXT를 합쳐 `21시`, `20분`, `10분 단위`, `Asia/Seoul`, `다음 주차`, `STD-MGT-03`, `24시`, `00분`이 모두 존재하는지 확인한다.

- [x] **Step 2: 구조 자동 검증**

  Description Num 수와 Callout 컨테이너 수가 각각 4개인지 확인한다. Callout이 잠금 해제 상태인지, 모든 TEXT의 absoluteBoundingBox가 프레임 범위를 벗어나지 않는지 확인한다.

- [x] **Step 3: 스크린샷 시각 검증**

  `1723:52`를 1800px 이상으로 캡처해 드롭다운이 입력 컨트롤로 인지되는지, 텍스트가 잘리지 않는지, 버튼 및 Description과 겹치지 않는지 확인한다.

- [x] **Step 4: 계획 완료 표시**

  Task 1–3의 체크박스를 완료로 바꾸고 Figma 노드 ID와 검증 결과를 완료 보고에 남긴다.
