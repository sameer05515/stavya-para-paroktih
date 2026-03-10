# stavya-para-paroktih

- **Topics**: `index.html` — browses `data/topics-export-flat.json`.
- **Interview questions**: `interview-questions.html` — browses `data/interview-questions-export-flat.json`.

## Run the UI

1. **With http-server**: from the project root run  
   `npm install` then `npm start`  
   (or `npx http-server -p 8080 -c-1`).  
   Open http://localhost:8080 for Topics or http://localhost:8080/interview-questions.html for Interview Questions.

2. **With another static server**: e.g. `npx serve .` then open http://localhost:3000.

3. **Without a server**: open `index.html` or `interview-questions.html` in your browser and use **Load from file** to choose the corresponding JSON from `data/`.