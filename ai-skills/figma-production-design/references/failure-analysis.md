# Failure Analysis

Use this reference when a previous Figma output looked wrong, too fake, or not production-ready.

## What Went Wrong In The Case Study

1. **Ambiguous "actual screen" interpretation**
   - The user wanted real product screens like a designer handoff file.
   - The work initially treated this as a high-fidelity visual mockup task and filled screens with stylized visuals.
   - Correct interpretation: build native UI layers and use explicit placeholders for unknown real content.

2. **Generated assets were applied too broadly**
   - The user allowed GPT-generated assets for service design-system elements such as weather cards, status icons, alerts, and profile/avatar assets.
   - Generated or hand-drawn visuals were incorrectly used to stand in for tourist imagery and map content.
   - Correct rule: generated assets are for service-owned UI assets only, not real-world content or external SDK output.

3. **Real media and external services were not modeled truthfully**
   - Tourist images and maps were drawn as fake scenic/map-like surfaces.
   - This made screens look populated but gave developers no clear integration contract.
   - Correct output: label these as `ExternalImageSlot` or `MapSDK` components with expected source/provider.

4. **Screens were built before enough system constraints**
   - Components existed visually, but screen construction did not consistently respect layout, z-order, and content constraints.
   - This caused issues such as buttons protruding from modals, score badges covering titles, and timeline lines covering icons.
   - Correct approach: define components and constraints first, then instantiate screens.

5. **QA was too generic at first**
   - Broad counts were checked, but screenshot-level issues remained.
   - Some overlap detection excluded or missed real visual problems.
   - Correct approach: combine programmatic QA with manual screenshot inspection, then run focused QA on affected screens.

6. **Layer order was not treated as a production requirement**
   - Timelines and map overlays need deliberate z-order.
   - A line can be geometrically correct but visually wrong if it sits above icons or text.
   - Correct approach: rails/dividers behind, dots/icons/text above, floating overlays above backgrounds.

## Prevention Rules

- Ask: "Would this region be rendered by our UI, loaded from content, or rendered by an SDK?"
- If loaded/rendered externally, never fake the final content unless asked.
- Make every screen region explain its implementation source.
- After every significant visual change, capture a page screenshot.
- Fix visible problems even if the automatic QA passes.
- When user points to an issue, inspect that exact screen and node category before broad refactoring.
