---
name: figma-production-design
description: Build or revise professional Figma design systems and production-ready app screens. Use when Codex is asked to create a Figma design system, component library, high-fidelity wireframes, product screens, mobile app screens, developer-handoff screens, or to improve PM wireframes into realistic production UI. Especially use when screens contain real media, external integrations, maps, SDK-rendered regions, generated service assets, or when visual QA for overlaps, clipping, z-order, and editability is required.
---

# Figma Production Design

Create production-grade Figma artifacts, not decorative mock images. Build design systems first, then assemble editable app screens from components, and validate visually and programmatically before finalizing.

Use this skill alongside Figma skills:
- Load `figma-use` before every `use_figma` call.
- Load `figma-generate-library` when creating foundations, variables, components, or assets.
- Load `figma-generate-design` when creating composed screens.

## Core Rule

Separate these three content types before drawing:

1. **Native UI**: buttons, tabs, cards, nav bars, chips, forms, lists, modals, scores, badges, headers. Build as editable Figma layers/components.
2. **Service design-system assets**: weather icons, alert state images, profile avatars, empty states, small status illustrations. Generated bitmap assets are allowed here when requested.
3. **External content regions**: tourist photos, real product images, maps, SDK surfaces, charts from another service, camera feeds, embedded media. Do not fake these with invented imagery. Replace them with explicit external-content components that identify the source or integration.

If a user says "actual screen" or references a polished Figma file, interpret that as production UI composition, not as permission to generate full-screen raster mockups.

## Workflow

1. **Define scope**
   - List screens and primary user flows.
   - Identify native UI, generated service assets, and external content regions.
   - If a referenced Figma file is inaccessible, say so and proceed from screenshots or user-provided references.

2. **Build the design system first**
   - Create foundations: color, type, spacing, radius, elevation, grid, icon sizing.
   - Create components: app shell, top bar, bottom nav, buttons, chips, cards, list rows, tabs, forms, modal, score badge, external image placeholder, map/SDK placeholder.
   - Keep generated assets in a separate asset section with labels and source notes.

3. **Create production screens**
   - Use one separate page for production screens, distinct from PM specs or annotated wireframes.
   - Build screens from native Figma layers/components.
   - Use generated bitmap assets only inside service asset components.
   - Use external-content placeholders for real media and integrations.
   - Avoid PM callouts, numbered annotations, and Description tables on production-screen pages.

4. **Validate before final**
   - Run programmatic QA for screen count, text overlap, clipped text, out-of-frame nodes, unexpected large raster images, fake media/map remnants, and z-order risks.
   - Capture a screenshot and inspect it manually.
   - Fix issues found by either QA or visual inspection, then re-run QA.

## External Content Placeholders

Use explicit components instead of fake images:

- `ExternalImageSlot / Hero`: "실제 이미지 연동", "홈 히어로 이미지", "CMS/API"
- `ExternalImageSlot / Thumbnail`: "실제 이미지", "관광지 API"
- `ExternalFeature / MapSDK`: "지도 SDK 영역", "Kakao/Naver Map", "경로·마커·현재 위치 렌더링"
- `ExternalFeature / Embedded`: name the provider or integration and expected rendered data.

Do not draw scenic substitutes, fake map routes, or fake screenshots unless the user explicitly asks for illustrative placeholders.

## Visual QA Requirements

Always check:

- Text does not overlap other text or critical UI.
- Text is not clipped and has enough width for Korean labels.
- Floating elements overlap only when intended: modal over scrim, floating map controls, bottom sheets.
- Timeline rails, route lines, and decorative dividers sit behind dots, icons, labels, and cards.
- Buttons remain fully inside their container unless intentionally floating.
- Image/SDK placeholders do not obscure screen copy.
- Score badges do not cover titles, thumbnails, or controls.
- Raster images are not used as full-screen UI.

Read `references/qa-checklist.md` for the concrete audit script patterns and issue categories.

## Failure Modes To Avoid

Before finalizing, read `references/failure-analysis.md` if the task involves revising an unsatisfactory design, turning PM wireframes into production screens, or replacing generated/fake imagery.

Key failures:

- Filling real-media regions with invented visuals.
- Treating "designer-level screen" as "make the whole screen look pretty" instead of "make it implementable and truthful."
- Creating components after screens instead of establishing the system first.
- Trusting generated layout without screenshot inspection.
- Not verifying z-order, especially timelines, map overlays, and modal buttons.

## Implementation Guidance

Read `references/figma-patterns.md` when writing Figma Plugin API code for this skill. It contains conventions for page structure, placeholder components, layer order, and targeted QA.

Return final results with:

- Figma page link.
- What was created or changed.
- Which regions are external-content placeholders.
- QA metrics and screenshot status.
- Any remaining limitations, especially inaccessible reference files or unavailable real assets.
