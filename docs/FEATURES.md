# Features and UX Behavior

This document explains what users can do on both pages.

## Shared features

- Tree navigation in left sidebar
- Search filtering with descendant-aware matching
- Theme toggle (light/dark)
- Sidebar show/hide
  - Mobile: drawer open/close
  - Desktop: collapse/expand (persisted)
- Prev/Next navigation (circular)
- URL hash deep-linking to selected node
- Load from local JSON file
- Markdown + HTML rendering
- Syntax highlighting in code blocks
- Copy button for each code block

## Topics page (`index.html`)

- Data source: `data/topics-export-flat.json`
- Detail panel includes:
  - Breadcrumb from `ancestors`
  - Topic title and optional description
  - Main `smartContent`
  - Topic sections (`sections[]`) as cards
  - Section metadata (`createdDate`, `updatedDate`) when available

## Interview Questions page (`interview-questions.html`)

- Data source: `data/interview-questions-export-flat.json`
- Detail panel includes:
  - Breadcrumb from `ancestors`
  - Question title/heading
  - Question rating (if present)
  - Main `smartContent`
  - Answers (`answers[]`) as cards
  - Answer rating (if present)

## Navigation details

- Prev/Next loops at boundaries.
- Selected item ID is synced to URL hash.
- On `hashchange`, UI updates selection if ID exists.

## Search behavior details

- Search checks current node text (`name` and `heading` for questions).
- Ancestors are preserved if descendants match.
- Tree expands relevant branches after filtering.

## Clipboard interaction

- Copy button appears at top-right of each `<pre><code>` block.
- Uses `navigator.clipboard.writeText` when available.
- Falls back to `document.execCommand('copy')`.
- Button feedback: `Copy` -> `Copied` (or `Failed`) -> reset.

