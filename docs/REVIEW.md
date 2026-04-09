# Review Notes (Current Snapshot)

Date: 2026-04-09

## Findings

### Medium: Duplicate inline implementation across both pages

- `index.html` and `interview-questions.html` each contain large inline CSS and JavaScript blocks with near-identical infrastructure code (theme, sidebar, code highlighting, code copy behavior, tree handling).
- This increases maintenance overhead and regression risk when future changes are applied to only one page.

**Recommendation**

- Extract shared concerns into `css/shared.css` and `js/*` modules:
  - theme
  - sidebar behavior
  - content rendering / markdown / highlighting
  - code-copy enhancement
- Keep page-specific logic in two thin app files.

### Low: Documentation drift in root README

- README examples mention port `8080` while `package.json` scripts run on `8081`.

**Recommendation**

- Keep all docs aligned to `8081`, or switch scripts back to `8080`.

### Low: Unused/empty directories

- `app/src`, `css/`, and `js/` currently exist but are empty in this snapshot.

**Recommendation**

- Either remove empty folders or complete modular migration so folder intent is clear.

## Regression checks performed

- Confirmed both pages include:
  - theme persistence
  - mobile/desktop sidebar behavior
  - search + nested match behavior
  - hash-based deep linking
  - code block copy button
  - JSON fetch + file-load fallback

No functional blocker found in this review pass.

