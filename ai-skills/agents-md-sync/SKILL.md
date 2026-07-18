---
name: agents-md-sync
description: Check and update AGENTS.md instruction files after work that may have happened outside Codex. Use when the user asks to verify, refresh, sync, or repair project agent instructions; it performs no-op reporting when instructions are already current, makes minimal updates for clear mismatches, and interviews the user when intent is ambiguous.
---

# AGENTS.md Sync

## Purpose

Keep `AGENTS.md` files aligned with the real project state so future agents receive accurate instructions. This skill is for checking whether existing guidance is still current, updating clear mismatches, and asking targeted questions only when the intended guidance cannot be inferred safely.

Use this skill when the user asks:

- `AGENTS.md 갱신`, `agents.md 체크`, `에이전트 지침 최신화`
- "I worked without Codex; check instructions"
- "sync project instructions", "refresh agent docs", "repair stale AGENTS"
- to verify folder structure, module entrypoints, commands, generated artifacts, or project rules reflected in `AGENTS.md`

## Operating Rules

- Respect all existing `AGENTS.md` scope rules while editing.
- Prefer no-op when current instructions match the project. Do not rewrite for style alone.
- Make the smallest clear update that fixes the mismatch.
- Preserve user-authored policy, safety rules, generated markers, runtime overlays, and local conventions.
- Never delete guidance just because it is not currently exercised. Remove or change it only when evidence shows it is stale or contradicted.
- Do not expose secrets, credentials, private tokens, machine-specific caches, or transient runtime paths as project guidance.
- Treat deeper `AGENTS.md` files as more specific than parent files.

## Workflow

1. **Find Scope**
   - Identify the repository/project root and all `AGENTS.md` files under the requested scope.
   - If no `AGENTS.md` exists and the user asked to check existing guidance, report that none exists. Create one only when the user asked to create/update guidance or the project clearly requires it.
   - Note nested scopes such as `docs/AGENTS.md`, `demo/AGENTS.md`, `video/AGENTS.md`, or similar module-level files.

2. **Gather Evidence**
   - Inspect current structure with `rg --files` or `find`, excluding `.git`, dependency folders, build output, caches, and runtime state.
   - Read project anchors when present: `README`, package/config files, docs indexes, module-level `AGENTS.md`, traceability docs, design docs, or scripts that define commands.
   - Check recent local changes when useful: `git status --short`, `git diff --name-only`, and untracked major folders/files.
   - Separate stable project facts from transient artifacts.

3. **Compare**
   - Compare `AGENTS.md` against current evidence for:
     - folder tree and module roles
     - module entrypoints and ownership boundaries
     - product scope, artifact types, and important terminology
     - build/test/verification commands
     - generated/local/ignored artifacts
     - rules for assets, docs, demos, videos, data, or skills
     - references to moved, renamed, or deleted files
   - For nested modules, check parent and child `AGENTS.md` together so they do not contradict each other.

4. **Decide**
   - **Current:** If all material guidance is current, make no file changes. Report "no changes needed" with the evidence checked.
   - **Clear mismatch:** If the correct update is obvious from files/docs, edit the relevant `AGENTS.md` files directly.
   - **Ambiguous:** If multiple reasonable interpretations exist, ask a concise user interview question before editing.

5. **Interview When Ambiguous**
   Ask only when the answer materially changes guidance. Common triggers:

   - A new folder exists but it is unclear whether it is permanent, generated, ignored, or experimental.
   - Docs and implementation disagree about product scope or commands.
   - A command exists but its intended verification role is unclear.
   - A module was renamed/moved but old references still appear in docs.
   - The project has personal/local assets that may or may not belong in shared guidance.
   - Updating guidance would change ownership, safety, or destructive-operation rules.

   Ask one to three short questions, then update from the answer. If only plain text is available, ask one focused question at a time.

6. **Edit**
   - Use `apply_patch` for manual edits.
   - Update only affected sections, usually folder structure, module entrypoints, verification commands, artifact boundaries, or project-specific rules.
   - Keep folder trees compact and high-signal. Do not list every generated file.
   - Preserve generated marker blocks and runtime overlays exactly unless the user explicitly asks to regenerate them.
   - If a new module gets a child `AGENTS.md`, also update the parent entrypoint/structure when that parent requires structure tracking.

7. **Verify**
   - Re-read changed sections.
   - Run `git diff -- AGENTS.md ...` or equivalent to confirm the patch scope.
   - Check for stale references with `rg` when paths/names changed.
   - If commands were added or changed, verify they exist in package/config files when practical.

## No-Op Criteria

Do not edit when:

- Folder structure and module descriptions already match material project state.
- New files are transient, generated, ignored, or clearly outside project guidance.
- The only difference is wording preference with no practical guidance effect.
- Evidence is ambiguous and the user has not answered the required interview question.

## Update Style

- Write in the language already used by the target `AGENTS.md`.
- Keep guidance operational: what to check, what to edit, what to avoid, what to run.
- Use stable categories rather than volatile file-by-file inventories.
- Prefer "when X changes, update Y" rules over one-off historical notes.
- Keep final guidance short enough that future agents can actually read it.

## Final Response

Report:

- `checked`: which `AGENTS.md` files and evidence sources were inspected
- `changed`: files updated, or "none"
- `why`: mismatch fixed, or why no-op was correct
- `verification`: diff/status/search/checks run
- `open question`: only if user input is still required

Example:

```text
확인 결과:
- checked: 루트 AGENTS.md, docs/AGENTS.md, README, package.json, docs index
- changed: 없음
- why: 폴더 구조/검증 명령/모듈 진입점이 현재 상태와 일치
- verification: rg 경로 확인, git diff 변경 없음
```
