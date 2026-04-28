Set up git correctly for this project. Run every step in order.

---

## 1. Fix git identity (local to this repo)

```bash
git config user.name "Yashvee"
git config user.email "yashvee814@gmail.com"
```

Verify global identity is also correct:
```bash
git config --global user.name "Yashvee"
git config --global user.email "yashvee814@gmail.com"
```

---

## 2. Check for a root .gitignore

If one does not exist, create it with these entries:
```
.env
.DS_Store
__pycache__/
*.pyc
.venv/
venv/
.claude/settings.local.json
```

---

## 3. Commit backend + infra to main

Stage ONLY these files:
- `README.md`
- `.env.example`
- `CLAUDE.md` (if it exists)
- `docker-compose.yml`
- `backend/`

Commit message format — subject line only, no Co-Authored-By:
```
Add backend API and project infrastructure
```

Push:
```bash
git push -u origin main
```

---

## 4. Create the frontend feature branch

```bash
git checkout -b feature/frontend
git add frontend/
git commit -m "Add React frontend"
git push -u origin feature/frontend
```

---

## 5. Show the PR link

Print the GitHub URL in this format so the user can open it in one click:
```
https://github.com/<owner>/<repo>/compare/main...feature/frontend?expand=1
```

Derive `<owner>` and `<repo>` from `git remote get-url origin`.

---

## 6. Verify everything looks correct

Run and show the output:
```bash
git log --pretty="%h %an <%ae> — %s" 
```

All commits must show `Yashvee <yashvee814@gmail.com>` as author.
If any commit shows a different author, rewrite it:
```bash
git filter-branch -f \
  --env-filter '
    export GIT_AUTHOR_NAME="Yashvee"
    export GIT_AUTHOR_EMAIL="yashvee814@gmail.com"
    export GIT_COMMITTER_NAME="Yashvee"
    export GIT_COMMITTER_EMAIL="yashvee814@gmail.com"
  ' \
  --msg-filter 'grep -v "Co-Authored-By:" || true' \
  HEAD
git push origin main --force
```
