# stavya-para-paroktih

Static UI for browsing exported knowledge data.

- **Topics UI**: `index.html` -> `data/topics-export-flat.json`
- **Interview Questions UI**: `interview-questions.html` -> `data/interview-questions-export-flat.json`

## Quick start

1. Install dependencies:
   `npm install`
2. Start local server:
   `npm start`
3. Open:
   - `http://localhost:8081/`
   - `http://localhost:8081/interview-questions.html`

If you open files directly (`file://`) and fetch is blocked, use **Load from file** on each page.

## Documentation

- `docs/ARCHITECTURE.md` - architecture and runtime model
- `docs/FEATURES.md` - user-facing behavior and UX details
- `docs/DATA-CONTRACTS.md` - input JSON contracts and expectations
- `docs/RUNBOOK.md` - run and troubleshooting guide
- `docs/REVIEW.md` - codebase review findings and recommendations

## License

MIT (see `LICENSE`).