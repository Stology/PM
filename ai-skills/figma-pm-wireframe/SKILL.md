---
name: figma-pm-wireframe
description: "Create or revise PM-facing Figma wireframe specification artifacts for any digital product: screen-spec wireframes with individually editable numbered callouts, Description tables, user-flow notes, feature/case frames, legacy-wireframe reuse, individually editable graph or relationship edges when needed, and final visual QA for callout/Description matching, text overflow, click blocking, and unintended overlaps."
---

# Figma PM Wireframe

## Purpose

Produce a PM wireframe specification in Figma, not a polished UI design. The artifact must help PMs, designers, and developers understand screen purpose, state/case variants, user actions, transitions, permissions, empty/error states, and implementation boundaries.

Use this skill when the user asks for:

- `PM 와이어프레임`, `화면설계서`, `화면 설계`, `wireframe specification`
- Figma artifacts based on a guideline/reference file
- feature-by-feature or case-by-case screen organization
- numbered callouts plus `화면설명(Description)` tables
- user-flow notes, screen IDs, screen paths, states, permissions, empty/error cases
- revising an existing or legacy wireframe to match new planning docs

## Core Inputs

Before building or revising, inspect the available project context. Do not assume a specific service structure.

1. Project instructions:
   - `AGENTS.md`, project README, or local workflow notes when present
   - user corrections in the latest messages; newer requests override older nonessential details
2. Product and planning docs:
   - PRD, product brief, planning doc, functional spec, change log, policy doc
   - screen requirements, IA, user-flow docs, acceptance criteria
   - MVP/deferred scope notes
3. Figma references:
   - guideline file or PM template file
   - legacy wireframe file, if the user wants reuse
   - target output file/page
4. Product-specific context:
   - service name, domain terms, user roles, permissions, platform, primary flows
   - brand/design-system constraints only where they affect wireframe clarity

If a project has specific files such as `docs/기획안.md` or `docs/wire_frame_requirements`, treat them as project-local inputs, not as assumptions baked into this skill.

## Figma Rules

- Load `figma:figma-use` before every `use_figma` call.
- Return created/mutated node IDs from every Figma write script.
- Keep PM wireframes mostly structural. Use brand color only as a restrained accent unless the user asks for a higher-fidelity artifact.
- Do not add unsupported features. Put excluded or deferred items only in an explicit out-of-scope/common-out frame or note.
- Preserve legacy layouts only when they still match the current docs and latest user intent.
- Remove obsolete service language from reused screens unless current docs explicitly require it.
- Keep annotations editable and click-safe: do not leave a page/frame-level `Callout Overlay` that groups all red numbers together. Prefer one unlocked group per number, named `Callout 1`, `Callout 2`, etc. This lets users select and edit each red number independently without a full-screen layer blocking the wireframe.

## Required Work Loop

For corrections or large PM wireframe updates, work page by page.

1. **Project profile**
   - Extract the product name, platform, core users, main objects, roles/permissions, lifecycle states, and MVP boundaries.
   - Build a short glossary from the docs and use those exact terms in screens and Description rows.
2. **Document map**
   - For each required frame, extract: screen purpose, visible UI elements, state/case variants, permissions, button behavior, destinations, empty/error text, and required Description rows.
   - When the workload is large and the user asks for parallel work, split analysis by independent feature groups. Example lanes:
     - entry/auth/onboarding/home
     - primary feature area A
     - primary feature area B
     - review/approval/reporting
     - settings/common states
   - Do not force these lanes; derive them from the product docs.
3. **Current Figma audit**
   - Inspect the target Figma page, frame list, and existing naming convention.
   - For every frame, compare the document map against visible UI, `화면설명(Description)`, red callout numbers, user-flow note, connectors, state variants, and modal/popup behavior.
   - Record mismatches before editing so corrections are traceable.
4. **Patch**
   - Update only what the docs or latest user correction require.
   - Rebuild or repair Description rows and callouts together, not independently.
   - Add missing case frames when they are in scope: empty state, loading, error, disabled submit, edit/delete modal, destructive confirmation, read-only/archived/ended state, permission-denied state, feedback/toast state.
5. **Verify**
   - Run an automated Figma audit.
   - Capture representative screenshots and visually inspect actual readability, not just node counts.

## PM Artifact Structure

Use a screen-spec layout that mirrors PM documentation:

```text
[Top Metadata Table]
Screen Path / 화면명
Screen ID / 기능 정의
Application to / Related docs

[Main Wireframe Area]
Platform frame, e.g. Web 1920 x 1080 or mobile size from docs
Left/center: actual wireframe
Right: 화면설명(Description)
Bottom/right: 사용자 플로우 note

[Annotations]
Numbered red callouts on UI areas
Matching Description rows
```

For feature grouping, arrange frames as feature/case sequences:

```text
01. Feature Main SCREEN_ID
01-01. Feature Empty STATE_ID
01-02. Feature Create MODAL_ID
01-03. Feature Error ERROR_ID
```

Prefer one feature row with detail/case frames left-to-right when working on a broad canvas. When editing an existing file, preserve the established frame grid unless the current structure blocks comprehension.

## Screen Coverage Planning

Derive screen coverage from the docs. Common groups to consider:

- Entry: login, signup, onboarding, invitation/deep-link entry
- Home/dashboard/list: first post-login view, cards, activity logs, recent items
- Create/edit/detail flows: form states, validation, success, failure, confirmation
- Shared container/navigation: sidebar, topbar, tabs, breadcrumbs, profile, global actions
- Primary feature screens: list, detail, filter, search, sort, panel, drawer, popup
- Input/import/upload flows when present: file, text, URL, validation, pending states
- Review/approval flows when present: candidate cards, reviewer status, approve/reject, disabled submit, done branches
- Reporting/analytics flows when present: summary, charts, pending/unavailable state
- Communication flows when present: comments, replies, questions, edit/delete, empty state
- Settings/share/invite flows when present: role-only actions, modal, copy feedback
- Common states: empty, loading, error, permission, read-only, archived/ended, toast/spinner/network failure

Do not create all groups by default. Include only what is supported by the product docs or user request.

## Reuse Policy

When a legacy Figma file exists:

- Reuse broad structure where still valid:
  - entry screen base
  - dashboard/card/list layout
  - shared navigation/header/tabs
  - primary data canvas or panel pattern
  - form/list/detail/review/report patterns
- Adapt terminology and interaction policy to current docs.
- Remove obsolete screens, labels, permissions, and states even if they exist in the old file.
- If the user's old wireframe intentionally reflects product thinking, preserve the spatial structure where it still matches the updated spec.

## Visual Construction Pattern

For product screens:

- Use the platform size stated in docs. If unspecified, web PM specs commonly use `1920 x 1080`; mobile specs should use the product's target device size.
- Keep visual style low/mid fidelity unless the user asks for high fidelity.
- Use a consistent shared layout for repeated surfaces: navigation, topbar, header, tabs, profile, global action area.
- For pre-auth screens, avoid post-auth navigation unless required.
- For post-auth screens, keep global navigation and profile placement consistent.
- For tabbed or multi-section products, keep tab order fixed across related frames once established by docs.

For numbered callouts:

- Put each red callout in its own unlocked group named `Callout 1`, `Callout 2`, etc.
- Each callout group contains exactly its matching circle and text:
  - `Callout Circle 1`
  - `Callout Text 1`
- Add the callout groups as the last children of the screen frame so they are never hidden behind other layers.
- Do not keep all callouts inside one page/frame-level `Callout Overlay` group in the final file. That makes the numbers feel page-level grouped and harder to edit individually.
- Do not use a full-frame transparent annotation frame in the final file. It can block selection of the real wireframe.
- Name children consistently:
  - `Callout Circle 1`
  - `Callout Text 1`
- Match numbers exactly to Description rows: `1..N`.
- Place callouts near the target UI, but not on top of readable text.
- Do not place callouts on button labels, form labels, table text, node labels, or other text that the PM/developer needs to read. If the target is a button or input, place the red circle just outside the component edge or in nearby whitespace.
- Avoid callout-to-callout overlap; move numbers apart even if they point to nearby UI.
- Users should be able to select/edit each callout directly in the final file. If clicking a red number selects all page callouts together, split them into per-number groups before delivery.

For relationship/graph/canvas screens:

- Add each connector as its own unlocked direct layer named `Graph Edge 1`, `Graph Edge 2`, etc.
- Do not leave all connectors inside one `Graph Connectors` frame/group in the final file. Users should be able to select and adjust each edge independently.
- Keep graph edges above the canvas background and below node labels/callouts.
- Make relationship states visually distinct when the docs require it, such as selected, related, active, inactive, source, target, warning, or disabled.

## Description Writing

Write implementation-ready text in the user's language. Korean is appropriate when the project docs/user request are Korean.

- Separate user-facing information from internal functional policy. Do not invent or force visible UI labels, columns, badges, helper boxes, or controls merely to expose aggregation rules, calculation criteria, lifecycle conditions, routing logic, permission checks, data-source notes, or other implementation details.
- When an internal rule affects the screen but does not need to be read or operated by the user, keep the wireframe UI faithful to the intended product surface and specify the rule in the existing `화면설명(Description)` row for the relevant callout. Create a new visible UI element only when the product docs or latest user request explicitly requires users to see or act on that information.
- In Description rows, state internal rules as concise, testable behavior, including trigger, inclusion/exclusion criteria, refresh/removal timing, destination, and exception handling where relevant.
- Buttons: state click behavior and destination.
- Lists/tables: define sort order, row contents, status badge behavior, pagination, and empty state.
- Forms: required/optional fields, validation, active/disabled CTA conditions, success/failure result.
- Modals/popups/drawers: open condition, confirm/cancel/close behavior, destructive confirmation.
- Permissions: prefer hiding unavailable actions; if visible, disable with reason.
- Read-only/archived/ended state: specify what remains viewable and what write actions are blocked.
- Out-of-scope features: keep out of the main UI and document separately.
- Keep Description rows semantically aligned with the red callout target. If red number `3` points to a list status badge, row `3` must describe that exact badge and behavior.
- Prefer concise, testable rows over broad prose. Include active/disabled/hidden behavior where relevant.

## Terminology

- Build a glossary from project docs before writing screen text.
- Use the product's own terms for objects, roles, actions, states, and permissions.
- Do not hard-code terms from previous projects.
- When revising a legacy file, replace obsolete labels with current glossary terms.

## Final QA Checklist

Run a Figma script audit and representative screenshots before claiming completion.

Required checks:

- Every frame has metadata appropriate to the chosen template: screen path/name, screen ID, purpose/function, related docs.
- Every frame has `화면설명(Description)` or equivalent explanation table and a user-flow note where the template requires it.
- Description row count equals red callout count.
- Description row numbers and callout numbers are exactly `1..N`, with no missing or duplicated numbers.
- Red callouts are direct per-number groups named `Callout N` at the top of each screen frame.
- No page/frame-level `Callout Overlay` remains in the final file unless the user explicitly wants grouped annotation editing.
- Each `Callout N` group is unlocked and contains one `Callout Circle N` plus one `Callout Text N`.
- Red callouts do not overlap each other.
- Red callouts do not cover readable text.
- Text does not leave its frame or component.
- Visible text does not unintentionally overlap.
- Shared navigation/header/tabs are consistent across related screens.
- Pre-auth and post-auth layouts do not accidentally mix states.
- Relationship/graph/canvas screens have visible individually editable `Graph Edge N` layers when connectors are part of the product concept.
- Modal foreground text is not confused with background screen text; use an opaque card/backdrop.
- If an automated overlap check reports modal/background coordinate collisions, confirm with screenshots that the foreground card/backdrop actually hides the background content.
- Final screenshots cover at least:
  - a main/home/list screen
  - one primary feature screen
  - one modal or popup
  - one complex state screen such as expanded/detail/review/error/read-only

Report final evidence with counts, for example:

```text
검수 결과:
- 전체 프레임: N개
- Description/빨간 번호 불일치: 0건
- 빨간 번호 레이어 가림: 0건
- 빨간 번호 개별 선택/편집 불가 또는 전체 오버레이 클릭 차단 문제: 0건
- 빨간 번호끼리 겹침: 0건
- 빨간 번호가 텍스트를 덮는 문제: 0건
- 텍스트 프레임 이탈: 0건
- 실제 보이는 텍스트 겹침: 0건
- 개별 편집 가능한 연결선: N개, 해당 시
```

## Delivery

Final response should be concise and include:

- target Figma file link or file/page name
- what changed
- QA evidence
- any known gap if a check could not run
