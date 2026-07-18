# Stology HyperFrames 영상 작업 지침

## Skills

This project uses AI agent skills for framework-specific patterns. Install them if not already present:

```bash
npx skills add heygen-com/hyperframes
```

Skills encode patterns like `window.__timelines` registration, `data-*` attribute semantics, Tailwind v4 browser-runtime styling for `--tailwind` projects, and shader-compatible CSS rules that are not in generic web docs. Using them produces correct compositions from the start.

## Commands

```bash
npm run dev          # preview in browser (studio editor)
npm run check        # lint + validate + inspect
npm run render       # render to MP4
npm run publish      # publish and get a shareable link
npx hyperframes docs <topic> # reference docs in terminal
```

## Project Structure

- `index.html` — main composition (root timeline)
- `design-improved/` — separate design-improved variant project with its own `index.html` and copied runtime assets
- `compositions/` — sub-compositions referenced via `data-composition-src`
- `assets/` — media files (video, audio, images)
- `meta.json` — project metadata (id, name)
- `transcript.json` — whisper word-level transcript (if generated)

## Linting — Always Run After Changes

After creating or editing any `.html` composition, run the full check before considering the task complete:

```bash
npm run check
```

Fix all errors before presenting the result.

## Key Rules

1. Every timed element needs `data-start`, `data-duration`, and `data-track-index`
2. Visible timed elements **must** have `class="clip"` — the framework uses this for visibility control
3. GSAP timelines must be paused and registered on `window.__timelines`:
   ```js
   window.__timelines = window.__timelines || {};
   window.__timelines["composition-id"] = gsap.timeline({ paused: true });
   ```
4. Videos use `muted` with a separate `<audio>` element for the audio track
5. Sub-compositions use `data-composition-src="compositions/file.html"`
6. Only deterministic logic — no `Date.now()`, no `Math.random()`, no network fetches

## Stology Video Production Notes

이번 세션에서 확인된 내용은 디자인 스타일 자체가 아니라, 영상 제작·연출 관점의 재발 방지 기준이다.

### Fixed Production Issues

- 오프닝 훅은 문서 아이콘이 단순히 쏟아지는 투박한 방식보다, 여러 앱/파일이 흩어지고 누적되는 흐름으로 “자료가 쌓인다”는 문제를 보여준다.
- 2번째 문제 제기 화면의 사람 표현은 CSS 도형 조합만으로 만들면 어색해질 수 있으므로, 영상 톤에 맞는 생성형 이미지/일러스트 에셋을 만들어 투명 PNG로 적용한다.
- 파일 업로드 장면은 문서를 드래그앤드롭 영역에 올린 뒤 문서 아이콘이 그대로 남지 않게 한다. 드롭 후 문서는 사라지고, 드롭 박스가 강조되었다가 복귀해야 한다.
- 팀 검토 화면은 승인/거절 버튼 클릭 후 해당 버튼의 활성 색상이 유지되어야 하며, 클릭 결과로 왼쪽 체크 표시가 순차 활성화되어야 한다.
- 팀 검토 화면의 `승인됨`, `검토중`, `거절됨` 상태 뱃지는 화면 밀도를 높이고 흐름을 방해하므로 제거한 상태를 유지한다.
- 지식 그래프 화면은 간선이 처음부터 연결된 상태여야 하며, 노드는 초기 상태부터 간선 위에 배치한다. 간선이 노드 위로 보이지 않도록 z-index를 유지한다.
- 그래프 노드는 “선이 그려지는” 연출보다, 이미 연결된 구조 위에서 노드가 하나씩 선명해지는 연출을 기본으로 한다.
- Evidence 패널, 그래프 노드, 텍스트 블록은 렌더 프레임에서 실제 겹침 여부를 확인한다. 특히 03 화면은 우측 목업 안에서 패널과 노드가 겹치지 않도록 좌표를 재검증한다.
- 스터디 리포트 화면의 “도넛차트” 텍스트 플레이스홀더는 실제 도넛차트 시각 요소로 대체한다.
- 로드맵 아이콘은 너무 빨리 등장하지 않게, 장면 전환 시간은 유지하면서 마지막 아이콘이 화면 전환 직전에 자연스럽게 도착하도록 stagger를 조절한다.
- 마지막 화면 하단 문구는 URL성 텍스트보다 행동 유도형 메시지로 사용한다.

### Direction for This Video

- 전체 구조는 60초 3막을 유지한다: 문제 인식 `0-15s` → 해결책 제시 `15-45s` → 미래 비전 `45-60s`.
- 핵심 메시지는 “쌓이기만 하는 자료를, 연결된 지식으로”이며, 모든 주요 컷에서 노드-엣지/연결/선명화 모티프를 반복한다.
- 기능 소개 컷은 `01`, `02`, `03`, `04` 번호 체계를 유지하고, 좌측 카피 + 우측 실제 화면/목업 구조로 통일한다.
- 장면별 모션은 “등장 → 핵심 인터랙션 → 정리/퇴장”이 분명해야 한다. 단순 정적 목업보다 드롭, 클릭, 체크, 활성화, 슬라이더 이동 같은 결과 중심 인터랙션을 넣는다.
- 텍스트는 한 컷에서 과도하게 길게 보이지 않게 줄바꿈을 직접 관리한다. 렌더 프레임에서 줄바꿈이 어색하면 문구 길이와 `<br>`을 조정한다.
- 실제 MP4 결과는 `npm run check`만으로 끝내지 말고, `npm run render` 후 `ffprobe`로 실제 duration을 확인하고 주요 타임스탬프 프레임을 추출해 육안 검수한다.

## Documentation

Full docs: https://hyperframes.heygen.com/introduction

Machine-readable index for AI tools: https://hyperframes.heygen.com/llms.txt
