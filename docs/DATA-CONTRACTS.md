# Data Contracts

This document describes the JSON contracts consumed by the two UI pages.

---

## Topics dataset

- File: `data/topics-export-flat.json`
- Consumed by: `index.html`
- Root type: `Topic[]`

### Topic shape (important fields)

```json
{
  "uniqueId": "string",
  "name": "string",
  "parentId": "string | null",
  "description": "string",
  "smartContent": {
    "content": "string",
    "textOutputType": "html | markdown | text",
    "textInputType": "string"
  },
  "ancestors": [
    { "uniqueId": "string", "name": "string" }
  ],
  "sections": [
    {
      "uniqueId": "string",
      "name": "string",
      "smartContent": {
        "content": "string",
        "textOutputType": "html | markdown | text"
      },
      "createdDate": "ISO date string",
      "updatedDate": "ISO date string"
    }
  ]
}
```

### Behavior expectations

- `uniqueId` must be unique across all items.
- `parentId = null` denotes a root node.
- Missing or empty `sections` is valid.
- `ancestors` is used for breadcrumb display.

---

## Interview questions dataset

- File: `data/interview-questions-export-flat.json`
- Consumed by: `interview-questions.html`
- Root type: `Question[]`

### Question shape (important fields)

```json
{
  "uniqueId": "string",
  "name": "string",
  "heading": "string",
  "parentId": "string | null",
  "order": "number | null",
  "rating": "number | null",
  "smartContent": {
    "content": "string",
    "textOutputType": "html | markdown | text",
    "textInputType": "string"
  },
  "ancestors": [
    { "uniqueId": "string", "name": "string" }
  ],
  "answers": [
    {
      "uniqueId": "string",
      "name": "string",
      "heading": "string",
      "rating": "number | null",
      "smartContent": {
        "content": "string",
        "textOutputType": "html | markdown | text"
      }
    }
  ]
}
```

### Behavior expectations

- Root questions have `parentId = null`.
- Child ordering uses:
  1) ascending `order` when available
  2) fallback lexical sort by `name`
- Missing `answers` is valid.

---

## Shared assumptions and validation

- Top-level JSON must be an array.
- Invalid/non-array payload triggers an "Invalid JSON structure" error UI.
- Non-existent IDs in URL hash are ignored.
- Content rendering supports mixed `textOutputType` safely for display.

## Practical guidance for exporters

- Keep `uniqueId` stable across exports for URL hash stability.
- Ensure parent IDs reference existing nodes.
- Preserve `ancestors` for accurate breadcrumbs.
- Avoid malformed HTML in `smartContent.content`.

