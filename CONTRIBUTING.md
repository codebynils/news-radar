# Contributing Guide for news-radar

Because this is a learning project I write this probably only for my future self.
The goal is to practice enterprise habits on a small codebase and leave future-me a clear trail.

---

## 1 · Project philosophy

- Keep each change **small, isolated, and reviewable**.  
- Treat the repo as a **teaching artifact**: clean commits, readable names, and up-to-date docs.

---

## 2 · Development workflow

1) **Create a branch from `main`:**

    ```bash
    git checkout -b feature/my-improvement
    ```

2) **Set up local environment:**

    ```bash
    docker compose up -d                 # start Kafka/Prometheus/Grafana (if defined locally)
    ./mvnw clean verify                  # backend build & tests
    (cd web && npm ci && npm run dev)    # frontend dev server
    ```

3) **Naming conventions**
   - Branch: `feature/...`, `fix/...`, or `docs/...`
   - Commits follow *Conventional Commits*:  
     - `feat(api): add cursor pagination`  
     - `fix(web): stabilize infinite scroll sentinel`

4) **Run all checks before merging:**

    ```bash
    ./mvnw verify
    (cd web && npm run lint && npm test -- --watch=false)
    ```

5) **Open a pull request (even for myself)**
   - Describe motivation, key changes, and how it was tested.  
   - Link or paste any screenshots / Grafana panels if relevant.  
   - Ensure CI is green.

---

## 3 · Code style & formatting

- **Java**: 2-space indentation, auto-format via Spotless/Google style.  
- **React/TS**: Prettier defaults (2-space, single quotes), ESLint strict.  
- **YAML/JSON**: 2-space indentation, trailing newline.  
- `.editorconfig` enforces basics (LF, final newline, no trailing spaces except in Markdown).

---

## 4 · Testing standards

- Prefer **behavioral tests** (end-to-end or vertical slice) over per-class tests.  
- Cover critical flows:
  - Ingest → Kafka → Process → Cosmos write (happy path + dedupe)  
  - API cursor pagination (newest page + “older than” with stable ordering)  
  - Web infinite scroll (loads next page on sentinel, no duplicates)
- Use **Testcontainers** for Kafka and Cosmos emulation where feasible.  
- Keep fixtures **small and deterministic** (minimal RSS samples).

---

## 5 · Documentation

- Update `README.md` when setup or behavior changes.  
- Record notable choices in `/docs/adr/` (Architecture Decision Records).  

---

## 6 · Release hygiene

- Tag milestones like `v0.1.0` when a demoable slice is complete.  
- Summarize changes in `CHANGELOG.md` (Keep a Changelog format).  

---

