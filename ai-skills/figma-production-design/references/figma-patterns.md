# Figma Patterns

Use these patterns when implementing production design screens via `use_figma`.

## Page Structure

Recommended pages:

- `00 Design System`
- `01 PM Wireframe Spec` if PM annotations are needed
- `02 Production App Screens`
- `03 Prototype / Flows` if interactions are requested

Keep production screens free of PM callouts and Description tables.

## Component Naming

Use descriptive names that expose implementation intent:

- `Button / Primary`
- `Card / Course`
- `ListRow / Itinerary`
- `ScoreBadge / Weather`
- `ExternalImageSlot / Hero`
- `ExternalImageSlot / Thumbnail`
- `ExternalFeature / MapSDK`
- `Modal / Alert`
- `Timeline / Rail`

## Placeholder Construction

External image placeholder:

- neutral surface
- small icon or source badge
- label such as `실제 이미지 연동`
- source hint such as `관광지 API`, `CMS 이미지`, or `홈 히어로 이미지`

Map/SDK placeholder:

- subtle grid or neutral map surface
- centered compact card
- provider and expected render responsibility
- no fake route geometry unless explicitly requested

## Generated Assets

Allowed:

- weather symbols
- alert/warning images
- state icons
- profile/avatar asset
- empty-state image
- small branded service illustration

Not allowed by default:

- complete app screens
- tourist/place photos
- map screenshots
- third-party rendered charts
- product screenshots from external services

## Figma API Notes

- Use `await figma.setCurrentPageAsync(page)`, not `figma.currentPage = page`.
- Load fonts before changing text.
- Return created/mutated node IDs from `use_figma`.
- Use `appendChild` and `insertChild` for z-order changes; do not assume convenience methods exist.
- After replacing children inside a frame, preserve the frame's size, parent, and semantic name.
- Avoid unsupported or hard-to-debug geometry for simple rails: rectangles are safer than rotated lines.

## QA Snippet Shape

For audits, traverse each target screen and collect:

- node name
- type
- text contents
- absolute or screen-relative bounding boxes
- parent name
- layer index

Then compute text intersections, clipped text, out-of-screen bounds, and unwanted fake visual remnants.
