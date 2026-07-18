# Design

## Source of truth
- Status: Active
- Last refreshed: 2026-05-29
- Primary product surfaces:
  - HyperFrames 영상 구성 `index.html`
  - 원본 제안서 PDF 기반 16:9 슬라이드 영상
  - 초반 후킹용 카카오톡 스타일 말풍선 오프닝
- Evidence reviewed:
  - `발표자료.pptx` — 16-slide final planning deck; palette refreshed to lavender/purple
  - `assets/pdf/stology-page-01.png` through `assets/pdf/stology-page-12.png` — PDF-rendered slide images at 1920 x 1081
  - `pdftotext Stology_Indigo_Editable.pdf` — slide copy and narrative structure
  - Existing `DESIGN.md` — replaced because it described a dark B2B SaaS style that does not match the PDF source deck
  - Current `index.html` — HyperFrames composition target that should inherit this visual system

## Brand
- Personality:
  - Structured, academic, calm, and operationally credible.
  - More “university club knowledge operating system” than generic SaaS advertisement.
  - Clear enough for a pitch deck, but still warm to Korean IT 동아리 members and 운영진.
- Trust signals:
  - Consistent top-left `Stology` wordmark.
  - Large, declarative Korean headlines.
  - Numbered process steps, comparison panels, and review/report UI mockups.
  - Evidence-driven language: 자료, 검토, 합의, 그래프, 리포트, 근거.
- Avoid:
  - Dark cyberpunk dashboards, heavy glows, neon grids, or futuristic sci-fi styling.
  - Generic stock SaaS dashboards unrelated to 동아리, 스터디, 학습자료, 팀 검토, or reports.
  - Playful consumer-chat colors beyond the brief hook section.
  - Overcrowded animation that competes with the PDF slide content.

## Product goals
- Goals:
  - Explain Stology as a knowledge-operations platform for IT clubs.
  - Show the problem: records are stored, but learning/project context is not connected.
  - Explain the solution: Study + Ontology turns weekly materials into a searchable knowledge structure.
  - Make the MVP journey legible: upload → AI extraction/review → knowledge graph → weekly report.
  - Preserve the source PDF’s pitch-deck credibility while making it video-native.
- Non-goals:
  - Do not redesign the PDF into an unrelated product website aesthetic.
  - Do not add unverified product features or screens absent from the PDF.
  - Do not turn the video into a dark, cinematic brand film.
- Success signals:
  - Viewers understand the problem within the first 5 seconds.
  - Slide content remains readable at 1920 x 1080.
  - The opening hook feels like a messaging thread, then transitions into the formal Stology deck.
  - The visual system reads as the same brand as the PDF.

## Personas and jobs
- Primary personas:
  - IT 동아리 파트장 / 스터디장: plans weekly study topics and monitors learning gaps.
  - 운영진: wants learning flow, review evidence, and weekly study records connected.
  - 동아리 멤버: wants to find past study materials and understand personal learning position.
  - 신입 멤버: needs fast context on what the club has already studied or built.
- User jobs:
  - Find prior materials quickly.
  - Understand what was learned, decided, or implemented.
  - Review AI-extracted knowledge candidates before they become trusted graph data.
  - Use weekly reports to choose the next study topic with evidence.
- Key contexts of use:
  - Pitch/demo video for a proposal or presentation.
  - Social or internal sharing where the PDF needs motion and a stronger opening hook.
  - 16:9 desktop/large-screen viewing first; mobile derivative possible later.

## Information architecture
- Primary navigation:
  - The video is linear, not navigational.
  - Narrative order should follow the PDF: title → problem → lived experience → disconnected knowledge → ontology → MVP flow → feature screens → positioning → expansion.
- Core routes/screens:
  - 자료 업로드
  - AI 추출 & 팀 검토
  - 지식 그래프
  - 주차별 리포트
  - positioning / expansion roadmap
- Content hierarchy:
  - Top-left brand wordmark.
  - Large headline in deep indigo.
  - Secondary explanatory copy in slate gray.
  - Process details in numbered rows, cards, tables, or UI mockup panels.
  - Bottom emphasis band or closing statement for key takeaway slides.

## Design principles
- Principle 1: Preserve pitch-deck clarity.
  - Slides should feel like a refined proposal deck: high contrast, generous margins, and deliberate hierarchy.
- Principle 2: Use indigo as the structural language.
  - Indigo is not decoration only; it defines headings, numbered markers, active states, buttons, bands, and graph emphasis.
- Principle 3: Motion supports comprehension.
  - Animate sequence and focus, not spectacle. Reveal questions, steps, and panels in reading order.
- Principle 4: Keep PDF fidelity high.
  - When using rendered PDF pages, do not crop away meaning. If zooming, zoom gently and keep the full slide recognizable.
- Tradeoffs:
  - Full-slide readability is prioritized over aggressive camera motion.
  - The chat-hook may use a messaging metaphor, but must bridge back to the formal indigo deck quickly.

## Visual language
- Color:
  - Page background: `#FBFAFF` / `#F8F4FF` — almost-white lavender from the final PPTX.
  - Primary ink: `#171421` — headline, logo, dark panels, strong text.
  - Primary purple: `#5B2DA5` / `#7030A0` — structural accents and dark purple surfaces.
  - Action violet: `#8B5CF6` — buttons, active markers, selected states, graph emphasis.
  - Soft lavender: `#EFE8FF` / `#DED7EA` / `#D7D0E8` — cards, dividers, graph edges, inactive-active gradients.
  - Secondary text: `#5F5872` / `#8B8499` — descriptions, metadata, muted labels.
  - White: `#FFFFFF` — clean panel surface and slide interior.
  - For the Kakao-style hook only: use muted yellow-green chat accents sparingly; keep Stology indigo present so it does not become off-brand.
- Typography:
  - Korean-first heavy sans-serif, matching the PDF’s geometric, bold presentation style.
  - Preferred stack: `Pretendard`, `Apple SD Gothic Neo`, `Noto Sans KR`, `Inter`, `system-ui`, sans-serif.
  - Headlines: very bold, large, tight tracking, deep indigo.
  - Body: medium weight, slate gray, generous line-height.
  - Labels/numbers: bold indigo, compact, used as structure markers.
- Spacing/layout rhythm:
  - 16:9 slide frame with generous outer margins around 90–110px at 1920px width.
  - Top-left wordmark appears consistently near the same optical anchor.
  - Major sections use two-column layouts, horizontal dividers, or large side-by-side panels.
  - Bottom key-message bars span almost full width with strong indigo fill and centered white text.
- Shape/radius/elevation:
  - Mostly flat presentation surfaces.
  - Subtle rectangular panels with low or no radius; UI mockups may use modest radii.
  - Avoid heavy shadows. If needed for video framing, use soft ambient shadow only around slide cards.
- Motion:
  - Use calm fades, slight upward drifts, sequential row reveals, and gentle scale-in for slide cards.
  - Hook bubbles should appear one-by-one like a chat thread: small vertical rise, opacity in, slight scale from 0.96 to 1.
  - For PDF pages, prefer subtle push-in/pan, progress bars, and section-by-section reveal overlays only when readability remains intact.
  - No bounce-heavy, elastic, or chaotic motion except very restrained chat-bubble easing.
- Imagery/iconography:
  - PDF uses soft 3D illustration on early problem slides, but the core system is typographic and diagrammatic.
  - Graph visuals should use pale periwinkle links, indigo active nodes, and gray inactive nodes.
  - Icons should be simple, line/label-based, and subordinate to text.

## Components
- Existing components to reuse:
  - PDF-rendered slide image cards from `assets/pdf/stology-page-*.png`.
  - Top-left `Stology` wordmark treatment.
  - Bottom indigo takeaway band.
  - Numbered process rows (`01`, `02`, `03`, `04`).
  - Comparison panels: current state vs Stology state.
  - Graph node/link diagrams.
  - Review UI mockup: node candidates, approve/reject controls, completion count.
  - Weekly report UI mockup: percentages, concept tags, recommendation area.
- New/changed components:
  - Opening chat hook using brand-safe Kakao-style bubbles.
  - Video slide wrapper that frames PDF pages without visually fighting the source deck.
  - Page progress rail for pacing if needed.
- Variants and states:
  - Active node: deep indigo fill, white text.
  - Weak active node: pale periwinkle fill, indigo text.
  - Inactive node: light gray fill, slate text.
  - Approved/reviewed: action indigo with check mark.
  - Pending/rejected: muted slate/gray, lower emphasis.
- Token/component ownership:
  - `DESIGN.md` owns visual tokens and rules.
  - `index.html` should implement tokens locally with CSS variables or clearly named classes.
  - Do not introduce a separate design-token package for this small HyperFrames project.

## Accessibility
- Target standard:
  - Aim for WCAG AA contrast for all newly authored text and overlays.
  - PDF-rendered slides should be displayed large enough for Korean body text to remain legible.
- Keyboard/focus behavior:
  - Not applicable to passive video playback, but source HTML should use semantic sections and meaningful `alt` text for PDF images.
- Contrast/readability:
  - Deep indigo on pale background is the core contrast pairing.
  - White text on primary indigo bars must stay large and bold.
  - Avoid placing small slate text over gradients or blurred illustration areas.
- Screen-reader semantics:
  - Each PDF image should have concise `alt` text describing slide purpose.
  - Decorative ambient layers should be ignored with `data-layout-ignore` and/or `aria-hidden` where applicable.
- Reduced motion and sensory considerations:
  - No flashing, strobing, or rapid oscillation.
  - Keep transitions smooth and deterministic.

## Responsive behavior
- Supported breakpoints/devices:
  - Primary composition: 1920 x 1080 landscape.
  - Source PDF images render as 1920 x 1081; fit with `object-fit: contain` or slight crop compensation only if necessary.
- Layout adaptations:
  - For landscape video, preserve full slide aspect and margins.
  - If later creating vertical/social cutdowns, rebuild layout per section instead of simply scaling the full PDF pages down.
- Touch/hover differences:
  - Not applicable to passive video.

## Interaction states
- Loading:
  - Not applicable in final rendered video; if previewing, assets should load locally from `assets/pdf`.
- Empty:
  - For product UI mockups, empty graph/project state is shown as pale/gray inactive nodes or a blank canvas.
- Error:
  - Not shown in the source PDF. Avoid inventing prominent error states for the video.
- Success:
  - Approved candidates, activated nodes, and generated reports should use strong indigo or check markers.
- Disabled:
  - Use gray/pale slate treatment for inactive graph nodes or unavailable concepts.
- Offline/slow network, if applicable:
  - Not applicable to this video.

## Content voice
- Tone:
  - Korean, direct, explanatory, and pitch-ready.
  - Use confident claims grounded in the PDF: “기록의 부재가 아니라 연결의 부재”, “자료가 지식 구조로 누적된다”, “검토로 신뢰 가능한 그래프”.
- Terminology:
  - Use `Stology`, `Study + Ontology`, `온톨로지`, `자료`, `지식 구조`, `노드`, `그래프`, `Evidence`, `검토`, `합의`, `주차별 리포트` consistently.
  - Preserve the team approval/rejection review comparison without naming developer-tool workflows.
- Microcopy rules:
  - Prefer short, declarative Korean lines.
  - Keep hook questions conversational, then shift into formal pitch language.
  - Do not over-explain what the visible PDF slide already says; video captions should add pacing or emphasis.

## Implementation constraints
- Framework/styling system:
  - HyperFrames HTML/CSS/GSAP in `index.html`.
  - Timed visible elements require `class="clip"`, `data-start`, `data-duration`, and `data-track-index`.
  - GSAP timeline must be paused and registered on `window.__timelines["main"]`.
- Design-token constraints:
  - Prefer CSS custom properties for palette values when editing `index.html`.
  - The canonical palette is light indigo, not dark cyan.
  - Do not use default Tailwind blues or generic dark SaaS colors unless mapped to this document.
- Performance constraints:
  - Keep PDF pages as local PNG assets.
  - Avoid network fetches, runtime randomness, or async timeline construction.
  - Avoid animating image dimensions; animate wrappers or transforms.
- Compatibility constraints:
  - Use deterministic GSAP only.
  - No `Math.random()`, `Date.now()`, or infinite `repeat: -1` animations.
- Test/screenshot expectations:
  - After editing `.html` compositions, run `npm run check`.
  - If `npm run check` cannot complete because npm registry access is unavailable, report that explicitly and run the nearest local/static checks possible.

## Open questions
- [ ] Should the final video include narration or remain silent with visual pacing only? / owner: user / impact: timing and caption density
- [ ] Should the PDF slides be shown full-frame for fidelity, or partially rebuilt as native HTML scenes for stronger motion? / owner: user / impact: production time and visual dynamism
- [ ] Is the opening Kakao-style hook intended to mimic actual KakaoTalk colors closely, or just use the chat metaphor while staying Stology-branded? / owner: user / impact: hook palette and bubble styling
