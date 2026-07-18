---
name: stology-figma-ia
description: Create or revise Stology IA pages in Figma. Use when asked to make an IA, information architecture, depth tree, page hierarchy, or to fix Stology IA spacing/connectors/labels in Figma based on the current planning and wireframe documents.
---

# Stology Figma IA

## Purpose

Produce a Stology IA page that can be reviewed without repeated visual correction. Build a depth-based tree structure in Figma, with connector geometry that is derived from card positions rather than eyeballed.

Use this skill together with the Figma `figma-use` workflow for write operations and screenshot verification.

## Source Order

Use project sources in this order before editing Figma:

1. `docs/기획안.md`
2. `docs/변경사항/합의_0514.md`
3. `docs/wire_frame_requirements/00-index.md`
4. Relevant `docs/wire_frame_requirements/0X-*.md`
5. Existing Figma IA or wireframe page metadata

Do not add MVP-excluded pages as normal IA nodes. Put them under a distinct `COMMON_OUT` or `MVP 제외` state if they must be shown.

## IA Structure

Use a depth tree, not a flowchart. Keep steps and depth separate:

- `0 Depth`: service root
- `1 Depth`: login, home, main entry
- `2 Depth`: study creation and study container
- `3 Depth`: study tabs and primary task areas
- `4 Depth`: modals, detail panels, states, and derived screens

For Stology, start from this baseline unless the source documents have changed:

- `0 Depth`: `Stology`
- `1 Depth`: `LGN001 로그인`, `HOM001 홈`
- `2 Depth`: `HOM010 스터디 생성 모달`, `STD000 스터디 컨테이너`
- `3 Depth`: `STD001 지식 구조 탭`, `UPL001 자료 업로드 탭`, `REC001 주차별 기록 탭`, `RPT001 주차별 리포트 탭`, `QNA001 질문함 탭`
- `4 Depth`: `STD010 노드 상세/자료 팝업`, `REV001 AI 후보 검토`, `MGT010 설정/운영 모달`, `COMMON 공통 상태`, `QNA010 질문 작성/수정`

## Canvas Layout

Use a wide frame when there are 5 depths. Prefer `2460 x 1210` or wider. A `1920 x 1080` IA frame is too tight for Stology once labels and right-side states are included.

Recommended column geometry:

```text
frame width: 2460
card width: 280
depth x positions: [100, 540, 980, 1420, 1960]
depth gap: 160
card height: 106, except root can be 118
```

Recommended y positions:

```text
root: 300
login: 270
home: 430
study create: 270
study container: 430
knowledge tab: 270
upload tab: 400
records tab: 530
report tab: 660
questions tab: 790
node detail: 270
review: 400
management: 560
common state: 720
question create/edit: 900
permission note: 1080
```

Keep at least `50px` vertical space between `COMMON 공통 상태` and `QNA010 질문 작성/수정`. Move the footer down instead of compressing these cards.

## Connector Rules

Build all cards first, then draw connectors from computed card edges. Do not place connectors by visual guessing.

Hard rules:

- Do not use text arrows such as `▶` as arrowheads. Use a real triangle/SVG arrowhead or a Figma vector shape.
- The arrowhead tip must land exactly on the target card's left edge.
- Horizontal line segments should stop before the arrowhead so they do not overshoot into the card.
- Remove old generated connectors before redrawing. Duplicate stale connectors are easy to miss in Figma screenshots.
- Draw labels after lines, so labels sit above the connector line.
- Every connector label's vertical center must match the connector line y-coordinate.
- For same-depth right-side targets, use one shared bend x-coordinate and one shared label-center x-coordinate.

Recommended connector constants for the geometry above:

```text
cardRight(depthN) = depthX[N] + 280
cardLeft(depthN) = depthX[N]
bus01 = 460
bus12 = 900
bus23 = 1340
bus34 = 1810
```

Use these center y values:

```text
root -> 1 Depth: 359
login: 323
home: 483
study create: 323
study container: 483
knowledge tab: 323
upload tab: 453
records tab: 583
report tab: 713
questions tab: 843
node detail: 323
review: 453
management: 613
common state: 773
question create/edit: 953
```

The auxiliary branch from `STD000 스터디 컨테이너` to `MGT010` and `COMMON` must run through the vertical midpoint between the upload card bottom and records card top. With the baseline geometry, this is `y = 518` because `UPL001` bottom is `506` and `REC001` top is `530`.

For `QNA001 질문함 탭 -> QNA010 질문 작성/수정`, use an elbow connector:

```text
from: questions card right edge at y=843
bend x: bus34
vertical segment: y=843 to y=953
to: question create/edit card left edge at y=953
label: 작성/수정 centered at x=bus34, y=953
```

## Label Rules

Place labels as small rounded rectangles centered on the line:

```text
label x = sharedCenterX - labelWidth / 2
label y = connectorY - 10
label height = 20
text y = connectorY - 7
```

Label widths:

- `생성`: 64
- `탭`: 48
- `검토 필요`: 78
- `스터디장`: 72
- `상태`: 52
- `작성/수정`: 72

For labels on the right-side 3-to-4 Depth area, align all label center x values to `bus34`. This prevents the "almost aligned" look that caused repeated visual corrections.

## Figma Write Workflow

When revising an existing IA:

1. Inspect the target page and frame IDs.
2. Remove generated IA connector nodes before redrawing.
3. If connector bugs are numerous, rebuild the IA frame internals rather than patching one segment at a time.
4. Create cards first.
5. Create connector lines and arrowheads from card edge coordinates.
6. Create labels last.
7. Select the IA frame and scroll into view.

Recommended generated node names:

- `Connector Line`
- `Arrowhead`
- `Connector Label BG`
- `Connector Label`
- `Card <ID>`
- `Title <ID>`
- `Desc <ID>`

These names let future runs safely remove and redraw only IA connector artifacts.

## Verification

Always capture a screenshot after editing the IA page. Do not report completion until the screenshot is checked for:

- Arrowheads touch target card left edges.
- No line is visually detached from the source card.
- Same-depth elbow bend x-coordinates match.
- Right-side label centers line up on the same x-coordinate.
- Each connector line passes through the vertical center of its label.
- `자료 업로드 탭` and `주차별 기록 탭` have equal-looking vertical spacing around the auxiliary branch.
- `공통 상태` and `질문 작성/수정` cards are not touching.
- The footer note does not overlap the bottom cards.
- No duplicate labels or ghost header text remains.

If a screenshot shows more than two connector defects, stop patching individual line segments. Rebuild the IA internals using the geometry in this skill.
