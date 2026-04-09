# Architecture

This repository is a static, client-side knowledge browser with two entry pages:

- `index.html` for topics (`data/topics-export-flat.json`)
- `interview-questions.html` for interview questions (`data/interview-questions-export-flat.json`)

## Runtime model

- No backend service is required for rendering.
- Data is loaded in-browser with `fetch(...)` from JSON files.
- If direct file access blocks fetch (`file://` CORS), users can load JSON via the **Load from file** control.
- Recommended local server: `http-server` (`npm start`) on port `8081`.

## UI stack

- Tailwind CSS via CDN (`https://cdn.tailwindcss.com`)
- Google Fonts (`DM Serif Display`, `Source Sans 3`)
- Markdown parsing via `marked`
- Syntax highlighting via `highlight.js`

## Page structure (both pages)

- Header
  - Sidebar toggle (mobile drawer + desktop collapse)
  - Search input
  - Theme toggle
  - File input ("Load from file")
  - Status text
- Sidebar tree
  - Hierarchical list from `parentId`
  - Expand/collapse behavior
  - Active item highlighting
- Main content area
  - Breadcrumb
  - Title/content rendering
  - Prev/Next navigation (circular)
  - URL hash synchronization

## State model

Both pages maintain these runtime structures:

- `items` array (`topics` or `questions`)
- `itemById: Map<string, Item>`
- `childrenByParentId: Map<string, Item[]>`
- `orderedIds: string[]` (DFS order)
- `currentId: string | null`

Persistent browser state:

- Theme in `localStorage.theme` (`light`/`dark`)
- Desktop sidebar collapse in `localStorage.sidebarCollapsed` (`true`/`false`)

## Rendering pipeline

1. Load data (`fetch` or `FileReader`)
2. Build indexes/maps
3. Render tree (with optional search filter)
4. Render detail view for selected hash item (if present)
5. Run code highlighting + copy button enhancement

## Search behavior

- Text search is case-insensitive.
- Parent nodes are retained if any descendant matches.
- Leaf nodes show spacer instead of chevron for alignment consistency.

## Content rendering rules

- `textOutputType === "markdown"` -> parsed with `marked`
- `textOutputType === "html"` -> rendered as HTML
- Questions page additionally supports plain text fallback
- Code blocks are highlighted and enhanced with copy-to-clipboard buttons

## Current implementation note

The current implementation is **inline-heavy**:

- CSS and JavaScript logic are duplicated across both HTML files.
- `css/` and `js/` directories exist in the repo but are currently empty.

For future maintainability, a shared-module split is recommended (see `docs/REVIEW.md`).

