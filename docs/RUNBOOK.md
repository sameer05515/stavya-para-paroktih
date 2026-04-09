# Runbook and Troubleshooting

## Prerequisites

- Node.js installed
- Dependencies installed:

```bash
npm install
```

## Start local server

The project is configured to run with:

```bash
npm start
```

Current script binds to `http://localhost:8081`.

## Open pages

- Topics: `http://localhost:8081/`
- Interview questions: `http://localhost:8081/interview-questions.html`

## Common issues

### 1) `GET /favicon.ico` 404

Expected previously if no favicon was configured.  
Current setup includes `favicon.svg`; hard refresh if browser still requests old icon path.

### 2) `Load failed` in UI

Likely causes:

- Local server is not running
- JSON path mismatch
- Opening via `file://` where `fetch` is blocked

Actions:

- Start `npm start`
- Verify JSON files exist under `data/`
- Use **Load from file** fallback

### 3) Port already in use (`EADDRINUSE`)

If `8081` is occupied:

- Stop the process using that port, or
- Temporarily run:

```bash
npx http-server -p 8082 -c-1
```

Then open pages on port `8082`.

### 4) Theme/siderbar state seems stuck

State is persisted in localStorage:

- `theme`
- `sidebarCollapsed`

Clear browser storage for the site to reset.

### 5) Code copy button does not work

- Clipboard APIs can be restricted in some browser contexts.
- Use HTTPS/localhost origin.
- Fallback (`execCommand`) is already implemented but may still be blocked by browser policy.

## Data import validation checklist

Before loading custom JSON:

- Confirm top-level value is an array
- Ensure every item has unique `uniqueId`
- Ensure `parentId` references valid nodes (or `null`)
- Ensure `smartContent.content` is a string

