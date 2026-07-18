# QA Checklist

Use this checklist before finalizing production Figma screens.

## Programmatic Checks

Run a `use_figma` audit that reports:

- `screenCount`
- external image slot count
- map/SDK slot count
- generated asset count
- large raster image count
- fake media/map remnants
- text overlap candidates
- clipped or narrow text candidates
- out-of-frame nodes
- PM artifact count on production pages

## Recommended Overlap Rules

Flag text overlap unless it is:

- status bar symbols
- intentional modal/scrim overlay
- external placeholder label inside its own placeholder
- icon-only single-character text

Do not ignore:

- score badges over titles
- card title over description
- weather icon over temperature
- button label outside button/container
- timeline rail over dots, icons, or labels
- map/SDK placeholder card obscuring modal copy

## Visual Screenshot Pass

Inspect at the same zoom where the user will review the file.

Check:

- Screen labels are readable and aligned.
- Mobile frames have consistent size and spacing.
- Headers do not collide with status bars.
- Top actions are inside the device frame.
- Bottom nav items are not clipped.
- Modal buttons are fully inside modal cards.
- Empty/external placeholders are clear but not visually dominant.
- Korean labels fit within chips, cards, and buttons.
- Floating elements are intentional and visually coherent.

## Targeted Re-Audit

When the user reports a specific issue:

1. Inspect only the affected screens first.
2. Query relevant nodes with names, positions, parent, and layer index.
3. Fix coordinates and layer order directly.
4. Capture a screenshot.
5. Re-run focused overlap/clipping QA for those screens.

## Layer Order Rules

- Background image/placeholder first.
- Decorative rails/dividers next.
- Cards, rows, thumbnails after rails.
- Dots, icons, labels above rails.
- Floating headers, bottom sheets, controls above content.
- Modals above scrims; modal buttons inside the modal bounds.
