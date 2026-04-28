Build a complete full-stack web application called "$ARGUMENTS" from scratch.

Follow every rule in CLAUDE.md exactly — tech stack, folder structure, file naming, code conventions, and Docker templates. Do not use placeholders. Every single file must be complete and immediately runnable.

---

## Step 1 — Clarify domain before writing any code

Ask the user ONE message:
- What does this app do? (one sentence)
- What are the main input fields the user will fill in?
- What should the AI analyse or return?

Wait for the answer, then proceed.

---

## Step 2 — Create all files in this exact order

1.  README.md
2.  .env.example
3.  CLAUDE.md  ← copy the CLAUDE.md from this repo verbatim
4.  backend/pyproject.toml
5.  backend/app/__init__.py
6.  backend/app/config.py
7.  backend/app/models.py   ← AdvisorRequest + ActionStep + AdvisorResponse (rename as appropriate)
8.  backend/app/llm.py      ← build_prompt() + async get_advice(), strip markdown fences, raise 502 on bad JSON
9.  backend/app/router.py   ← GET /health + POST /assess
10. backend/app/main.py     ← FastAPI app + CORS middleware
11. backend/Dockerfile
12. frontend/package.json   ← use Vite 5.4.x, NOT Vite 8
13. frontend/tsconfig.json
14. frontend/vite.config.ts
15. frontend/tailwind.config.js
16. frontend/postcss.config.js
17. frontend/.gitignore
18. frontend/index.html
19. frontend/src/index.css
20. frontend/src/types/<feature>.ts
21. frontend/src/api/<feature>.ts
22. frontend/src/components/LoadingSpinner.jsx
23. frontend/src/components/<Feature>Form.jsx
24. frontend/src/components/ResultCard.jsx
25. frontend/src/App.jsx    ← two-column layout, banner, background, error banner
26. frontend/src/main.jsx
27. frontend/Dockerfile
28. docker-compose.yml

---

## Step 3 — App layout rules (always apply)

- Sticky banner at the top: app name + tagline + status pill ("Local AI Active" with green pulse dot)
- Background: a CSS gradient that matches the domain theme (no external image URLs)
- Two-column grid on desktop (`lg:grid-cols-2`): form on left, results on right — no page scroll needed
- Placeholder panel on the right before first result: SVG illustration + instructional text
- Mobile: columns stack vertically
- White cards for form and result with `shadow-2xl ring-1 ring-black/5`

---

## Step 4 — Git setup (run after all files are written)

```bash
git config user.name "Yashvee"
git config user.email "yashvee814@gmail.com"
git add README.md .env.example CLAUDE.md docker-compose.yml backend/
git commit -m "Add backend API and project infrastructure"
git push -u origin main
git checkout -b feature/frontend
git add frontend/
git commit -m "Add React frontend"
git push -u origin feature/frontend
```

Then show the GitHub URL to open the PR.

---

## Step 5 — Final output

Show exactly three things:
1. The 3 terminal commands to run the app locally
2. How to verify Ollama is running (`curl http://localhost:11434/api/tags`)
3. A curl command to test the backend POST /assess endpoint
