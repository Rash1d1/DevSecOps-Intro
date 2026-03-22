# Triage Report — OWASP Juice Shop

> **Before submitting:** Run these commands, then paste outputs and complete checkboxes below:
> 1. `docker run -d --name juice-shop -p 127.0.0.1:3000:3000 bkimminich/juice-shop:v19.0.0`
> 2. Browse to http://localhost:3000 and take a screenshot → save as `labs/screenshots/juice-shop-home.png`
> 3. `curl -s http://127.0.0.1:3000/rest/products | head` → paste output in Health Check
> 4. `curl -I http://127.0.0.1:3000` → check for CSP/HSTS in Surface Snapshot

## Scope & Asset

- Asset: OWASP Juice Shop (local lab instance)
- Image: bkimminich/juice-shop:v19.0.0
- Release link/date: [v19.0.0 Release](https://github.com/juice-shop/juice-shop/releases/tag/v19.0.0) — 2025-09-04
- Image digest: sha256:37cc73163c4c269c044e890fee868d62637109cad126a26dab13dc442ef2ae76

## Environment

- Host OS: Linux 6.8.0-58-generic
- Docker: 26.1.3, build 26.1.3-0ubuntu1~24.04.1

## Deployment Details

- Run command used: `docker run -d --name juice-shop -p 127.0.0.1:3000:3000 bkimminich/juice-shop:v19.0.0`
- Access URL: http://127.0.0.1:3000
- Network exposure: 127.0.0.1 only [x] Yes [ ] No _(bound to localhost only)_

## Health Check

- Page load: 
  - **Screenshot path:** `labs/screenshots/juice-shop-home.png` _
- API check: Output from `curl -s http://127.0.0.1:3000/rest/products | head`:

```
<html>
  <head>
    <meta charset='utf-8'> 
    <title>Error: Unexpected path: /rest/products</title>
    <style>* {
  margin: 0;
  padding: 0;
  outline: 0;
}
```

## Surface Snapshot (Triage)

- Login/Registration visible: [x] Yes [ ] No e)_
- Product listing/search present: [x] Yes [ ] No 
- Admin or account area discoverable: [x] Yes [ ] No 
- Client-side errors in console: [ ] Yes [x] No _
- Security headers (quick look): `curl -I http://127.0.0.1:3000` → CSP/HSTS present? 
**No**
```
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Feature-Policy: payment 'self'
X-Recruiting: /#/jobs
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Sun, 08 Feb 2026 13:47:06 GMT
ETag: W/"124fa-19c3d818e94"
Content-Type: text/html; charset=UTF-8
Content-Length: 75002
Vary: Accept-Encoding
Date: Sun, 08 Feb 2026 13:57:38 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```

## Risks Observed (Top 3)

1) **SQL Injection** — Juice Shop is intentionally vulnerable; search, login, and product endpoints may accept unsanitized input leading to database exposure.
2) **Cross-Site Scripting (XSS)** — Client-side rendering with user-supplied data may allow script injection in product reviews, search, or feedback forms.
3) **Weak Authentication / Broken Access Control** — Admin functionalities and user data may be accessible without proper authorization checks.

---

## Task 2 — PR Template Setup

### 2.1: Creation Process

The PR template was created at `.github/pull_request_template.md` with the required sections:
- **Goal** — Purpose of the PR
- **Changes** — Summary of modifications
- **Testing** — How changes were verified
- **Artifacts & Screenshots** — Evidence and attachments

And a checklist with 3 items:
- [ ] Clear, descriptive title
- [ ] Documentation updated if needed
- [ ] No secrets or large temp files committed

### 2.2: Template Verification

- PR template was added to the **main** branch first (per bootstrap note: GitHub loads templates from the default branch).
- Branch `feature/lab1` was created for the lab submission.
- When opening a PR from `feature/lab1` → `main`, the template auto-fills in the PR description.

### 2.3: Workflow Impact

PR templates improve collaboration by:
- **Consistency** — Every PR follows the same structure, making reviews faster.
- **Completeness** — Required sections (Goal, Changes, Testing, Artifacts) remind contributors to document their work.
- **Checklists** — Explicit checks (e.g., no secrets) reduce common mistakes and enforce standards.

---

## Task 6 — GitHub Community Engagement

### GitHub Community

**Why starring repositories matters in open source:** Stars act as both bookmarks and social signals—they help you discover and revisit useful projects, indicate community trust and popularity, and encourage maintainers. They also surface on your profile, showing your interests to others.

**How following developers helps:** Following professors, TAs, and classmates lets you see their activity, discover new projects through their work, and build professional connections. It supports learning from experienced developers and staying updated on course-related contributions.

---
